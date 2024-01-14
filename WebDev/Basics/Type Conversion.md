#### String Conversion

The `String()` function converts different values to strings:
![[Pasted image 20240113114039.png]]

#### Numeric Conversion

The `Number()` function converts different values to numbers:
![[Pasted image 20240113114246.png]]
Explicit conversion is usually required when we read a value from a string-based source like a text form but expect a number to be entered.

If the string is not a valid number, the result of such a conversion is `NaN`. For instance:
![[Pasted image 20240113114323.png]]

Numeric conversion rules:
![[Pasted image 20240113114355.png]]


#### Boolean Conversion

Boolean conversion is the simplest one.

It happens in logical operations but can also be performed explicitly with a call to `Boolean(value)`.

The conversion rule:
- Values that are intuitively "empty", like `0`, an empty string, `null`, `undefined`, and `NaN`, become `false`.
- Other values become `true`.

For instance:
![[Pasted image 20240113114711.png]]
