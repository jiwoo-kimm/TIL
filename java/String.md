# String
* package `java.lang.String`
* extends `Object` class

## Method

### `compareTo()`

- Compares two strings lexicographically, based on the Unicode value of each character
- Returns 0 if two are equal
- Returns a value less than 0 if this string is lexicographically less than the argument
- Returns a value greater than 0 if this string is lexicographically greater than the argument

### `matches()`

- Tells whether or not this string matches the given **regular expression**

### `replace()`

- Returns a string resulting from replacing **all occurrences** of oldChar in this string with newChar
- Returns a reference to this string if oldChar does not occur in this string

### `split()`

- Splits this string around matches of the given **regular expression**
- Returns the array of strings computed by splitting this string around matches of the given regular expression

### `substring()`

- Returns a string that is a substring of this string with the beginIndex and endIndex
- Throws `IndexOutOfBoundsException` if beginIndex is negative or larger than the length of this String object

### `strip()`

- Returns a string whose value is this string, with all **leading and trailing** white space removed
- **white space**
- 공백, '\n', '\t', '\f', '\r', and other seperators on Unicode
+) `stripLeading()`, `stripTailing()`

### `trim()`

- Returns a string whose value is this string, with all leading and trailing space removed
- **Space** is defined as any character whose codepoint is less than or equal to 'U+0020' (the space character)

> `trim()`은 Unicode 값에 따라 처리하지만, `strip()`은 `isWhiteSpace()`라는 보다 정교한 메소드를 거친 결괏값을 바탕으로 문자열을 처리한다. 따라서, `strip()`이 좀 더 정확한 `whiteSpace` 범위를 갖기 때문에 `strip()`을 쓰는 것이 바람직하다.
