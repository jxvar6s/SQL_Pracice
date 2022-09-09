# Numric Type 

# Numeric Data Types.

## Integer Types Supported by MySQL

| Type      | Storage (Byte)  | Minimum Value Signed   | Minimum Value Signed | Maximum Value Signed | Maximum Value Unsigned |
|:------    |:--------|:-------------- |:-------------|:---------------|:---------------|
|TINYINT    |	1	  | -128	       | 0	          | 127	           | 255            |    
|SMALLINT   |	2	  | -32768	       | 0	          | 32767	       | 65535          |
|MEDIUMINT  |	3	  | -8388608	   | 0	          | 8388607	       | 16777215       |
|INT	    |   4	  | -2147483648	   | 0	          | 2147483647	   | 4294967295     |
|BIGINT	    |   8	  | $-2^{63}$	   | 0	          | $2^{63}$-1	   | $ 2^{64}$-1    |

## Fixed-Point Types (Exact Value) - DECIMAL, NUMERIC

The DECIMAL and NUMERIC types store exact numeric data values. These types are used when it is important to preserve exact precision, for example with monetary data. In MySQL, NUMERIC is implemented as DECIMAL, so the following remarks about DECIMAL apply equally to NUMERIC.

In a DECIMAL column declaration, the precision and scale can be (and usually is) specified. For example:
```bash
hourly_pay DECIMAL(6,3)
```

In this example, 5 is the precision and 2 is the scale. The precision represents the number of significant digits that are stored for values, and the scale represents the number of digits that can be stored following the decimal point.

Standard SQL requires that DECIMAL(5,2) be able to store any value with five digits and two decimals, so values that can be stored in the salary column range from -999.99 to 999.99.

If the scale is 0, DECIMAL values contain no decimal point or fractional part.

The maximum number of digits for DECIMAL is 65, but the actual range for a given DECIMAL column can be constrained by the precision or scale for a given column. When such a column is assigned a value with more digits following the decimal point than are permitted by the specified scale, the value is converted to that scale. (The precise behavior is operating system-specific, but generally the effect is truncation to the permissible number of digits.)

## Floating-Point Types

The FLOAT and DOUBLE types represent approximate numeric data values. MySQL uses four bytes for single-precision values and eight bytes for double-precision values.

For FLOAT, the SQL standard permits an optional specification of the precision (but not the range of the exponent) in bits following the keyword FLOAT in parentheses; ; that is, FLOAT(p). MySQL also supports this optional precision specification, but the precision value in FLOAT(p) is used only to determine storage size. A precision from 0 to 23 results in a 4-byte single-precision FLOAT column. A precision from 24 to 53 results in an 8-byte double-precision DOUBLE column.

## Bit-Value Type - BIT

The BIT data type is used to store bit values. A type of BIT(M) enables storage of M-bit values. M can range from 1 to 64.

Bit values are specified by b('vlue')

If you assign a value to a BIT(M) column that is less than M bits long, the value is padded on the left with zeros. For example, assigning a value of b'101' to a BIT(6) column is, in effect, the same as assigning b'000101'.

## Numeric Type Attributes.

The display width does not constrain the range of values that can be stored in the column. Nor does it prevent values wider than the column display width from being displayed correctly. For example, a column specified as SMALLINT(3) has the usual SMALLINT range of -32768 to 32767, and values outside the range permitted by three digits are displayed in full using more than three digits.

When used in conjunction with the optional (nonstandard) ZEROFILL attribute, the default padding of spaces is replaced with zeros. For example, for a column declared as INT(4) ZEROFILL, a value of 5 is retrieved as 0005.

The ZEROFILL attribute is deprecated for numeric data types, as is the display width attribute for integer data types

All integer types can have an optional (nonstandard) UNSIGNED attribute. An unsigned type can be used to permit only nonnegative numbers in a column or when you need a larger upper numeric range for the column. For example, if an INT column is UNSIGNED, the size of the column's range is the same but its endpoints shift up, from -2147483648 and 2147483647 to 0 and 4294967295.

> For more information about Numeric Types.  [MySQL Data Types Documentation](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)