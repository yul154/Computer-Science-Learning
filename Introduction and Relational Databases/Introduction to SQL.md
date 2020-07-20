# SQL
* DML: SELECT, INSERT, DELETET, UPDATE
* DDL: CREATE, DROP

<img width="508" alt="Screen Shot 2019-03-27 at 1 57 10 PM" src="https://user-images.githubusercontent.com/27160394/55100433-471f5e80-5098-11e9-8cdb-3ac05dacd2fb.png">

## SELECT
```
select Attributs
from Table
where condition
```

* Combine two relations
```
select distinct sName,major # distince delete duplicate value 
from student, Apply
where Student.sID=Apply.sID # JOIN condtion
```
```
selection sname,GPA,decison
from Student,Apply
where Student.sID=Apply.sID and sizeHS<1000 and major='CS' and cname='Stanford'
```

* Ambiguous common attribute
```
select cName # both of college and apply have cName, covert to College.cName
from College,Apply
where College.cName=Apply.cName and enrollment>20000 and major='CS'
```
* Order results by one attribute or a set of attributes
```
select Student.sID,sName,GPA,Apply.cName,enrollment
from Student,College,Apply
where Apply.sID=Student.sID and Apply.cName=College.cName order by GPA desc, enrollment
```
* Predicate(string matching on attribute values)
```
select sID,major
from Apply
where major like '%bio%'
```
* present all attribute by `*`
* define attribute you want to see
```
select sID,sName,GPA,sizeHS,GPA*(sizeHS/1000/0) as scaledGPA
from College
```
## Table variables and set operators

* Table name
```
select S.sID,sName,GPA,A.cName,enrollment
from Student S,College C,Apply A
where A.sID=S.sID and A.cName=C.cName
```
```
# join two same table
select S1.sID,S1.sName,S1.GPA,S2.sID,S2.sName,S2.GPA
from Student S1, Student S2
where S1.GPA=S2.GPA and S1.sID<S2.sID
```
* Set operators
1.Union: by default, eliminates duplicates in its results
```
select cName from College
union # add all will present duplicates
selection sName from Student
```
2. intersect
```
select distinct sID from Apply where major='CS'
intersect
select sID from Apply where major='EE';
```
3. exception
```
# who have applied to major in CS, but have not applied to major in EE.
select sID from Apply where major='CS'
except
select sID from Apply where major='EE';

select distinct A1.sID # there is possible that one student who applied CS AND EE AND Others
from Apply A1, Apply A2
where A1.sID=A2.sID and A1.major='CS' and A2.major<>'EE';

select sID,sName 
from Student
where sID in (select sID from apply where major='CS') and sID not in (select sID from apply where major='EE')

select sID,sName# there is possible that one student who applied CS AND EE AND Others
from student
where sID=any(select sID from Apply where major='CS') and sID<>any(select sID from Apply where major='EE')

select sID,sName
from student
where sID=any(select sID from Apply where major='CS') and not sID=any(select sID from Apply where major='EE')

```

## WHERE
* subquerise: nested select statements
  * Compare with `join`, subquerise would not raise duplicate problem
```
# ID's and names of all students who have applied to major in CS to some college.
select sID, sName
from Student
where sID in (select sID from Apply where major='CS')
```
```
select S.sID,S.sName # one studet who applied multiple cs， add distinct would delete different studet with same name
from Student S,Apply A
where S.sID=A.sID and major='CS'
```

```
select sID,sName 
from Student
where sID in (select sID from apply where major='CS') and sID not in (select sID from apply where major='EE')


```
  * exist: to check whether a subquery is empty or not empty rather than checking whether values are in the subquery.
```
# all college such that some othe college is in the same state
select cName, state
from College C1
where exists (select * from College C2 where C2.state=C1.state C1.cName=C2.cName)
```

```
# Student with highest GPA
select sName,GPA
from Student S1
where not exist( select * from Student S2 where S1.GPA<S2.GPA)

select sName,GPA
from Student S
where GPA>=all(select GPA from Student)

select sName,GPA# if highest value is uniqle
from Student S1
where GPA > all ( select GPA from Student S2 where S1.sID<>S2.sID)

select sName,GPA# whereas any is true if the condition is satisfied with one or more elements of the sub-query.
from Student S1
where not GPA <= any ( select GPA from Student S2 where S1.sID<>S2.sID)
```

```
# Students not from the smallest high school
select sID,sName,sizeHS
from Student
where sizeHS>any(select sizeHS from Student)

select sID,sName,sizeHS# instead of any, using `exist`
from Student S1
where exists(select * from Student S2 where S2.sizeHS<S1.sizeHS)
```
## FROM AND SELECT
```
# Students whose scaled GPA changes GPA bu more than 1
select sID,sName,GPA,GPA*(sizeHS/1000.0) as scaledGPA
from student
where abs(GPA*(sizeHS/1000.0)-GPA>1.0)

select *
from (select sID,sName,GPA,GPA*(sizeHS/1000.0) as scaledGPA from Student) G
where abs(G.scaledGPA-GPA)>1.0
```
* When you write a sub-query in the `select clause`, it's critical that sub-query return exactly one value, because the result
of that is being used to fill in just one cell of the result.
```
# Colleges paired with the highest GPA of their applications

select College.cName,state,GPA
from College,Apply,Student
where College.cName=Apply.cName and Apply.sID=Student.sID and GPA>=
all(select GPA 
from  Apply,Student
where College.cName=Apply.cName and Apply.sID=Student.sID)

select cName,state,
(select distinct GPA
from Apply,Student
where College.cName=Apply.cName and Apply.sID=Student.sID and GPA>=
all(select GPA from  Apply,Student
where College.cName=Apply.cName and Apply.sID=Student.sID)) as GPA
from College

select cName,states, # when we get a bunch of values in the result, which one to put in the tuple that's being constructed.
(select distinct sName
from Apply, Student
where  College.cName=Apply.cName and Apply.sID=Student.sID) as sName
from College;
```
## Aggergation
> min, max, sum, avg, count

* min, avg
```
select avg(GPA)# same student apply multiple different CS
from Student,Apply
where Student.sID=Apply.sID and major='CS'

select avg(GPA)
from Student
where sID in (select sID from Apply where major='CS')
```
* count: count number of tuple
```
# the number of colleges
select count(*)
from College
where enrollment>15000
```
```
select count(distinct sID)
from Apply
where cName='Cornell'
```
```
# Amount by which average GPA of CS students exceeds averages of not CS students
select CS.avgGPA-NonCS.avgGPA
from (select avg(GPA) as avgGPA from Student 
      where sID in 
       (select sID from Apply where major='CS')) as CS
     (select avg(GPA) as avgGPA from Student 
      where sID not in 
       (select sID from Apply where major='CS')) as nonCS
      
select disinct(select avg(GPA) as avgGPA from Student 
      where sID in 
       (select sID from Apply where major='CS')) -
     (select avg(GPA) as avgGPA from Student 
      where sID not in (select sID from Apply where major='CS'))
      )
from Student
```
* `Group by`: only used in conjunction with aggregation
```
select cName,count(*)
from Apply
group by cName

select state, sum(enrollment)
from college
group by state

# Minimum and Maximum GPA of applications to each college and major
select cName, major, min(GPA),max(GPA)
from Student, Apply
where Student.sID=Apply.sID
group by cName,major

# Number of colleges applied to by each student

select Student.sID, count(distinct cName)
from Student, Apply
where Student.sID=Apply.sID
group by Student.sID
```
* when we include in the select clause of a grouping query, again if we go back to group by, and we put in the select clause an attribute that's not one of the grouping
attributes. It actually chooses a random value from the group to include

```
# Number of colleges applied to by each student(some of them didn't apply any school)
select Student.sID,count(distinct cName)
from Student, Apply
where Student.sID=Apply.sID
grouyp by Student.sID
union
select sID, 0
from Student
where sID not in(select sID from Apply)
```
* having clause: after the group by clause and it allows us to check conditions that involve the entire group.
```
# colleges with fewer than 5 applicants

select cName
from Apply
group by cName
having count(*)<5

select distinct cName
from Apply A1
where 5>(select count(*) from Apply A2 where A1.cName=A2.cName)

```

##  NULL VALUES
* `count` would not count NULL value
*  compare operations would not count NULL value
* when we right select the distinct GPA.We do include the null

## DATA modification statements
> insert, delete, update

* Insert
```
insert into Table
value (v1,v2,v3)

insert into table
selection statement
```
```
insert into Apply
select sID,'CMU','CS',NULL
from Student
where sID not in (select sID from Apply)
```
```
# admit CMU EE all students who were turned down in EE else where
insert into Apply
select sID 'CMU','EE','Y'
from Student
where sID in (select sID from Apply where major='EE' and decision='N')
```
* delete
```
delete from table
where condition
```
```
# delet all students who applied to more than two different majors
delete from Student
Where sID in (select sID
from Apply
group by sID
having count(distinct major)>2)
```
```
delete from College
where cName not in (select cName from Apply where major='CS')
```
* update
```
update table
set attr=expression
where condition

update table
set a1=expre1, a2=expre2...
where condition
```
```
update Apply
set decision='Y', major='economics'
where cName='CMU'
and sID in(select sID from Student where GPA<3.6)
```
```
update Apply
set major='CSE'
where major='EE'
and sID in
(select sID from Student
where GPA>=all
(select GPA from Student
where sID in(select sID from Apply where major='EE')))
```
```
update Student
set GPA=(select max(GPA) from student), sizeHS=(select min(sizeHS) from Student)
```

## JOIN
* Inner join on *condition* == theta join
1. join operator only be binary
```
select distinct sName,major
from Student, inner join Apply
on Student.sID=Apply.sID
```
2.join only for binary
```
# JOIN THRE TABLE
select Apply.sID, sName, GPA,Apply.cname,enrollment
from (Apply join Student on Apply.sID=Student.sID and ) join College
ON Apply.cName=College.cName
```
* Natural join: don't need explicity present common attributes
1. natural join eliminate duplicate attribute names
```
select distinct sName,major
from Student,Apply
where Student.sID=Apply.sID

select distinct sName,major
from Student, natural join Apply# natural join automatically apply equality 
```
```
select sName, GPA
from Student join Apply
on Student.sID=Apply.sID
where sizeHZ<1000 and major='CS'and cName='Standford'
```
* Inner Join *using* (attrs): explicitly lists the common attribues
1. same name but not equated: natural join implicity combines columns that have same name
```
select sName, GPA
from Student join Apply using(sID)
where sizeHZ<1000 and major='CS'and cName='Standford'
```
2. don't allow to have both `using` clause and an `on` clause(change to `where`)
3. any relations joined with itself gives you back the original relation

* outer join(left,right,full)
1. left outer join(dangling tuple):dangling tuple with no right matching tuple, still added to the result with NULL values
```
# some student didn't apply any school yet
select sName,sID,cName,major
from Student left outer join Apply using(sID)# join Student table

# without outer join operator
select sName,sID,cName,major
from Student,Apply
where Student.sID=Apply.sID
union
select sName,sID,NULL,NULL
from Student
where sID not in (select sID in Apply)
```
2. right outer: mathcing all right table tuples
```
# sID without name
select sName,sID,cName,major
from Student natureal right outher Apply
```
3. full outer: union
```
select sName,sID,cName,major
from Student full outer Apply

select sName,sID,cName,major
from Student right outher Apply using(sID)
union
select sName,sID,cName,major
from Student left outher Apply using(sID)

select sName,sID,cName,major
from Student,Apply
where Student.sID=Apply.sID
union
select sName,sID,NULL,NULL
from Student
where sID not in (select sID in Apply)
union
select NULL,sID,cName,major
from Apply
where sID not in (select sID in Student)
```
<img width="762" alt="Screen Shot 2019-03-28 at 7 40 39 PM" src="https://user-images.githubusercontent.com/27160394/55199725-68b04100-5191-11e9-9b6b-5af1b98c4d41.png">

* outer join is not associativety((A op B) op C =A op(B op C))
