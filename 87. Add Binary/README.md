这道题从思路上算是简单题，但处理的时候细心一点，没太大问题。

两个字符串，肯定从尾部开始迭代起，时刻计算三个东西：a 的当前位(abit)，b 的当前位(bbit)，进位(carry)。

那么计算后 ret 的当前位即为：
```cpp
// 奇数为1，偶数为0
ret = (abit + bbit + carry) & 0x1 : "1" : "0" + ret;
//  或者可以直接使用 XOR
ret = abit ^ bbit ^ carry : "1" : "0" + ret;
```

计算后进位即为：
```cpp
carry = abit + bbit + carry >= 2; // 只需判断是否大于2即可
```

最后，迭代的时候要注意，短的字符串迭代完，继续判断长的字符串，若长短都判断完，还有进位要判断。故循环条件显然应该是：`apos || bpos || carry`，不存在的当前位，用 `0x0` 来替代运算即可。

为了节省字节数，我使用的 bool 来进行全程操作，你也可以采用 short or int.