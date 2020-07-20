# Data representation
## Computer work in binary
* very easy to distinguish on and off
* easily sample to tell what we have
* Hexadecimals(based 16): Binary is very hard fo people to deal with(two many digits), want a more compressed representation
  * Every 4 binary digits can be representated Hex digit(grouping of 4)
  * If i have four bits i have 0 through 15
  * Byte=8 bites
  * the basic size of data that system deals with easily is 64 bites

## Bit-level manipulation

### Bitewise Operation
> & ~ |
* take single bite and view it true or false
* And: A&B: if both are 1, True
```
 0100101
&0110100
 0100100
```
* Or: A|B: either A OR B, True
```
 0100101
|0110100
 0110101
```
* Not: ~A=1, when A=0
```
~001001
 110110
```
* Exclusive-Or(Xor): A^B=1 when A=1 or B=1, but not both
```
 0100101
^0110100
 0010001
```
### logic operations
> &&, ||, !
* Take the whole integer and view it true or False
* If all the bites are zero, it's False, if any bit is one, it's True

### Shift operations
* left shift(x<<y): shove zeros to the right(push to left)
  * shift bit-vector x left y positions(throw away extra bits on left, fill with 0s on right)
* right shift(x>>y): just the reverse
  * logical shift(applied with unsigned value): fill with 0s on left
  * arithmeic shift(applied with signed value): replicate most significant bit on left(if 1 on leftmost, fill with 1)
* Undefined Behavior: shift amount <0 o >= len

## Encoding intergers
### representastion: unsigned(B2U) and signed(B2T)
* Unsigned : hold a larger positive value and no negative value
* Signed integers: can hold both positive and negative numbers.
* Two's complement(singed value)
  * the left-most-bit to identify if the number is positive or negative
  * nonnegative is 0, negative is 1 
```
10=01010
-10=11010
```
* Numeric ranges:
  1. unsigned values: 0-->2^n-1(000000-111111)
  2. signed values: -2^n-2-->2^n-2(100000-011111)
  3. Umax = 2* Tmax + 1, |Tmin| = Tmax + 1
<img width="841" alt="Screen Shot 2019-03-20 at 6 53 59 PM" src="https://user-images.githubusercontent.com/27160394/54724538-efd23900-4b41-11e9-95ce-28ec9ce1ed8c.png">

* Constants: By default are considered to be signed value, Unsigned if have 'U' as suffix
* Casting surprises:
 1. unsigned value if mixture(implicity)
 2. including comparsion operations(<,>,==,<=,>=)
```
c1=-1,c2=0U
c1>c2(unsigned)#c1 convert to unsigned
```
### Sign Extension
> given w-bit signed integer x, convert it to w+k bit integer with same value
* Make k copys o sign bit
<img width="622" alt="Screen Shot 2019-03-20 at 7 22 02 PM" src="https://user-images.githubusercontent.com/27160394/54725476-9b30bd00-4b45-11e9-92d4-a938400cfc96.png">

### Truncation
> given k+w-bit signed integer x, convert it to w bit integer with same value
* drop k top bits

## Addition, negation,mutlplication,shifting

### Addition
* Unsigned addtion: ignore carry output
<img width="503" alt="Screen Shot 2019-03-21 at 5 50 52 PM" src="https://user-images.githubusercontent.com/27160394/54787425-10fa5e80-4c02-11e9-94cb-cfabb16d49e9.png">

* Two complement addtion: Tadd and Uadd have identical bit-level behavior
 * Overflow: at most once
 1. if sum>2^w-1, become negative
 2. if sum<-2^w-1, become postive

## Multiplication
> computing product of w-bit numbers x,y
### signed multiplication in C
 1. ignores high order w bits
 2. 
### power of 2 mutiply: 
> u << k == u * 2^k
* if i want mutiply, i left shift, if i want divide, i right shift
* shift operation are faster than multiply operation
* u<<3==u * 8
* complier automatically convert multiply to bit shift




