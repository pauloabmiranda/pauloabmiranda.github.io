---
layout: page
title: Bitwise operators - fast integer math
categories: as3
published: true
---

**Left bit shifting to multiply by any power of two**

Approximately 300% faster.

`x = x * 2;`<br>
`x = x * 64;`

`//equals:`

`x = x << 1;`<br>
`x = x << 6;`

**Right bit shifting to divide by any power of two**

Approximately 350% faster.

`x = x / 2;`<br>
`x = x / 64;`

`//equals:`
`x = x >> 1;`<br>
`x = x >> 6;`

**Number to integer conversion**

Using int(x) is 10% faster in AS3. Still the bitwise version works better in AS2.

`x = int(1.232)`

`//equals:`<br>
`x = 1.232 >> 0;`

**Extracting color components**

Not really a trick, but the regular way of extracting values using bit masking and shifting.

`//24bit`<br>
`var color:uint = 0x336699;`<br>
`var r:uint = color >> 16;`<br>
`var g:uint = color >> 8 & 0xFF;`<br>
`var b:uint = color & 0xFF;`

`//32bit`<br>
`var color:uint = 0xff336699;`<br>
`var a:uint = color >>> 24;`<br>
`var r:uint = color >>> 16 & 0xFF;`<br>
`var g:uint = color >>>  8 & 0xFF;`<br>
`var b:uint = color & 0xFF;`

**Combining color components**

‘Shift up’ the values into the correct position and combine them.

`//24bit`<br>
`var r:uint = 0x33;`<br>
`var g:uint = 0x66;`<br>
`var b:uint = 0x99;`<br>
`var color:uint = r << 16 | g << 8 | b;`

`//32bit`<br>
`var a:uint = 0xff;`<br>
`var r:uint = 0x33;`<br>
`var g:uint = 0x66;`<br>
`var b:uint = 0x99;`<br>
`var color:uint = a << 24 | r << 16 | g << 8 | b;`

**Swap integers without a temporary variable using XOR**

Pretty neat trick, it is explained in detail in the link at the top of the page. This is 20% faster.

`var t:int = a;`<br>
`a = b;`<br>
`b = t;`

`//equals:`<br>
`a ^= b;`<br>
`b ^= a;`<br>
`a ^= b;`

**Increment/decrement**

This is much slower than the pre/post decrement operator, but a nice way to obfuscate your code ;-)

`i = -~i; // i++`<br>
`i = ~-i; // i--`

**Sign flipping using NOT or XOR**

Strangely enough, this is 300%(!) faster.

`i = -i;`

`//equals`<br>
`i = ~i + 1;`

`//or`<br>
`i = (i ^ -1) + 1;`

**Fast modulo operation using bitwise AND**

If the divisor is a power of 2, the modulo (%) operation can be done with:
modulus = numerator & (divisor - 1);
This is about 600% faster.

`x = 131 % 4;`

`//equals:`<br>
`x = 131 & (4 - 1);`

**Check if an integer is even/uneven using bitwise AND**

This is 600% faster.

`isEven = (i % 2) == 0;`

`//equals:`<br>
`isEven = (i & 1) == 0;`

**Absolute value**

Forget Math.abs() for time critical code. Version 1 is 2500% faster than Math.abs(), and the funky bitwise version 2 is again 20% faster than version 1.

`//version 1`<br>
`i = x < 0 ? -x : x;`

`//version 2`<br>
`i = (x ^ (x >> 31)) - (x >> 31);`

**Comparing two integers for equal sign**

This is 35% faster.

`eqSign = a * b > 0;`

`//equals:`<br>
`eqSign = a ^ b >= 0;`

**Fast color conversion from R5G5B5 to R8G8B8 pixel format using shifts**

`R8 = (R5 << 3) | (R5 >> 2)`<br>
`G8 = (R5 << 3) | (R5 >> 2)`<br>
`B8 = (R5 << 3) | (R5 >> 2)`

