
[[]+{} 和 {}+[]](https://stackoverflow.com/questions/9032856/what-is-the-explanation-for-these-bizarre-javascript-behaviours-mentioned-in-the/9033306#9033306)

1. `[] + []`

使用相加的操作符时，左右两边的操作数会先转换为基本类型。转换一个对象类型到基本类型，会返回它的默认值，对于拥有`toString()`方法的对象会返回调用`object.toString()`的结果。对于数组结果和调用`array.join()`相同，拼接一个空数组会返回空字符串，因此相加操作会拼接两个空字符串，所以结果为空字符串。

2. `[] + {}`

和`[] + []`类似，两个操作数会先转换为基本类型，对于对象，同样是调用`object.toString()`的结果，因此结果是`"[object Ojbect]"`。

3. `{} + []`

这里涉及到两种情况，根据不同的浏览器处理方法有所不同。

第一种，浏览器将`{}`作为代码块进行解析，因此这是空的代码块会进行忽略，相当于处理`+[]`，对于`+`操作符，等同于`ToNumber(ToPrimitive(operand))`，空数组转换为基本类型为空字符串，`ToNumber("")`结果为0。

第二种情况，同`[] + {}`的解析过程，只是操作数进行了对调，因此结果还是`"[object Ojbect]"`。

4. `{} + {}`

同样涉及到两种情况，根据不同的浏览器处理方法有所不同。

第一种，浏览器还是将`{}`作为代码块进行解析，相当于处理`+{}`，同`{} + []`的第一种处理方式，实际上就是处理`ToNumber("[object Object]")`，结果是`NaN`。

第二种，处理的是两个空对象的相加，首先对加号两侧的操作数进行基本类型的转换，利用`object.toString()`方法转换后为`"[object Object]" + "[object Object]"`，因此结果就是字符串的拼接`[object Object][object Object]`。