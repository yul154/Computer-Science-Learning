# Character Class

* Primitive data types is char, Java provides wrapper class `Character` for `char`

```
char ch = 'a';
char [] carray= {'a','b','c','d'};
Character cha = new Character('a');
```

## Escape Sequences

|Escape Sequences| Descriptionn|
|----------------|-------------|
|\t|Inserts a tab in the text at this point.|
|\b| Inserts a backspace in the text at this point.|
|\n|Inserts a newline in the text at this point.|
|\r|Inserts a newline in the text at this point.|
|\f|Inserts a form feed in the text at this point.|
|\'|Inserts a single quote character in the text at this point.|
|\"|Inserts a double quote character in the text at this point.|
|\\|Inserts a backslash character in the text at this point.|

## Character Methods

| Method| Description|
|-------|-------------|
| `isLetter()`|Determines whether the specified char value is a letter.|
|`isDigit()`|Determines whether the specified char value is a digit.|
|`isWhitespace()`|Determines whether the specified char value is white space.|
|`isUpperCase()`|Determines whether the specified char value is uppercase.|
|`isLowerCase()`|Determines whether the specified char value is lowercase.|
|`toUpperCase()`|Returns the uppercase form of the specified char value.|
|`toLowerCase()`|Returns the lowercase form of the specified char value.|
|`toString()`|Returns a String object representing the specified character value that is, a one-character string.|

---

# Strings class

* Strings are a sequence of characters.
* Strings are treated as objects.

### Creating strings
1. direct create
```
String s = "hello ,world";
```
2. create as an object
```
char [] hearray= { 'h', 'e', 'l', 'l', 'o', '.'};
String hs = new String(hearray);// hello.
```
## String Buffer & String Builder class
> Modify Strings

* the main difference between the StringBuffer and StringBuilder
  * `StringBuilders` methods are not thread safe (not synchronised).
  * It is recommended to use `StringBuilder` whenever possible because it is faster than `StringBuffer`.

### String Buffer methods
1. `append()` : updates the value of the object that invoked the metho
```
StringBuffer sBuffer =  new StringBuffer("test");
sBuffer.append(" add");
System.out.println(sBuffer); // test add
```

2. `reverse()`
> reverses the value of the StringBuffer object that invoked the method.
```
StringBuffer buffer = new StringBuffer("Game Plan"); 
buffer.reverse();
```
3. `delete()`
> removes the characters in a substring of this StringBuffer
```
public StringBuffer delete(int start, int end)
```
4. `insert()`
```
sb.insert(3,"123");
```

5. `replace()`
> replaces the characters in a substring of this StringBuffer with characters in the specified String.

```
public StringBuffer replace(int start, int end, String str)
```
* if the length of str > end-start+1: direct add
*  if the length of str < end-start+1: delete rest of characters

6.`length()`
>returns the number of characters contained in the string object

* obtain information about an object are known as accessor method

7. `format()`
> print output with formatted numbers.

```
String fs;
fs = String.format("The value of the float variable is " +
"%f, while the value of the integer " + "variable is %d, and the string " +
"is %s", floatVar, intVar, stringVar);
System.out.println(fs);
```
---
## String methods

1. `chartAt()`
> returns the character located at the String's specified index
```
public char charAt(int index)
```

2. `compareTo(Object o)`
>  compares this String to another Object.

* Lexicographically compare

```
 int compareTo(Object o)
 int compareTo(String anotherString)
 int compareToIgnoreCase(String str)
```
3. `concat()`
> appends one String to the end of another.

```
 public String concat(String s)
```
* returns a string that represents the concatenation of this object's characters followed by the string argument's characters.

4. `contentEquals()`
>  returns true if and only if this String represents the same sequence of characters as specified in StringBuffer.

```
 public boolean contentEquals(StringBuffer sb)
```

5. `copyValueOf(char[] data)`
> returns a String that represents the character sequence in the array specified.

```
 public static String copyValueOf(char[] data)
 public static String copyValueOf(char[] data, int offset, int count)
```

6. `endsWith()` & `startsWith()`
> tests if this string ends with the specified suffix.
```
public boolean endsWith(String suffix)
public boolean startsWith(String prefix)
Str.endsWith("immutable")
Str.startsWith("Welcome")
```

7. `equals()`
> compares this string to the specified object
```
 public boolean equals(Object anObject)
 public boolean equalsIgnoreCase(String anotherString)
```

8. `getBytes(String charsetName)`
> encodes this String into a sequence of bytes using the named charset, storing the result into a new byte array.

```
public byte[] getBytes(String charsetName) throws UnsupportedEncodingException
```

* This method returns the resultant byte array.

9. `getChars()`
>  copies characters from this string into the destination character array.
```
public void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)

String Str1 = new String("Welcome to real world"); 
char[] Str2 = new char[7];
Str1.getChars(2, 9, Str2, 0);
```

10. `hashCode()`
> returns a hash code for this string.

```
 public int hashCode()
```

11. `indexOf(int ch)`
> returns the index within this string of the first occurrence of the specified character or -1
```
 public int indexOf(int ch )
 public int indexOf(int ch, int fromIndex)
 int indexOf(String str)
 int indexOf(String str, int fromIndex)
```
12.`Intern()`
>  returns a canonical representation for the string object
* This method ensures that all the same strings share the same memory.

13 `lastIndexOf(int ch)`
> returns the index of the last occurrence of the character in the character sequence represented by this object that is less than or equal to fromIndex, or -1
```
 int lastIndexOf(int ch)
 public int lastIndexOf(int ch, int fromIndex)
 public int lastIndexOf(String str)
 public int lastIndexOf(String str, int fromIndex)
```

14. `matches()`
> whether or not this string matches the given regular expression. 
```
public boolean matches(String regex)
public boolean regionMatches(int toffset,String other,int ooffset,int len)
public boolean regionMatches(boolean ignoreCase,int toffset,String other,int ooffset,int len)
```

15. `replace()`
> returns a new string resulting from replacing all occurrences of oldChar in this string with newChar.
```
public String replace(char oldChar, char newChar)
```

16.`replaceAll()`
> replaces each substring of this string that matches the given regular expression with the given replacement.
```
public String replaceAll(String regex, String replacement)
```
17.`replaceFirst()`
> replaces the first substring of this string that matches the given regular expression with the given replacement.
```
public String replaceFirst(String regex, String replacement)
```
18.`split()`
> splits this string around matches of the given regular expression.
```
 public String[] split(String regex, int limit)
```

19. `subsequence()`
>  returns a new character sequence that is a subsequence of this sequence.

```
public CharSequence subSequence(int beginIndex, int endIndex)

String str = "welcome world";
String nstr = str.subSequence(2,4)
```
* CharSequence is an interface and String is a concrete class. 

20.`substring()`
> eturns a new string that is a substring of this string. The substring begins with the character at the specified index and extends to the end of this string or up to endIndex – 1, 

```
public String substring(int beginIndex, int endIndex)
```

21. `toCharArray()`
>  converts this string to a new character array.
```
public char[] toCharArray()
```

22. `toLowerCase()` & `oUpperCase() `
> converts all of the characters in this String to upper or lower case
```

public String toUpperCase()
public String toLowerCase()
```

23. `trim()`
> returns a copy of the string, with leading and trailing whitespace omitted.
```
 public String trim()
 String str = "   welcome world";
 System.out.println(str.trim());//welcome world
```

24. `valueOf()`
> returns the string representation of the passed argument.

```
static String valueOf(datatype data)
```
