# ['1', '2', '3'].map(parseInt) what & why ?

前置知识：

- array的map方法，传入的三个参数依次是item、index和数组本身
- `parseInt(string, radix)`
  - string是必要的需要被解析的字段
  - radix表示要解析字段的基数（一般省略或者为0 的时候基数为10，即10进制，值在2-36之间）

- 其他应该注意：当参数 *radix* 的值为 0，或没有设置该参数时，parseInt() 会根据 *string* 来判断数字的基数。

  举例，如果 *string* 以 "0x" 开头，parseInt() 会把 *string* 的其余部分解析为十六进制的整数。如果 *string* 以 0 开头，那么 ECMAScript v3 允许 parseInt() 的一个实现把其后的字符解析为八进制或十六进制的数字。如果 *string* 以 1 ~ 9 的数字开头，parseInt() 将把它解析为十进制的整数。

  ```shell
  parseInt('10')	//10
  parseInt('12',3)	//4 (1*3+2*0)
  parseInt('11',2)	//3 (1*2+1*0)
  parseInt("1f",16);		//返回 31 (16+15)
  parseInt("010");		//未定：返回 10 或 8
  ```

  

解析`['1', '2', '3'].map(parseInt)`:

> `['1', '2', '3'].map(parseInt)`相当于返回 `parseInt('1',0)` `parseInt('2',1)` `parseInt('3',2)`,所以，三个返回值分别为`1` `NaN` `NaN`,所以结果是`[1,NaN,NaN]`

同理：`['10','10','10','10','10'].map(parseInt);`的返回值是`[10,NaN,3,4,5]`;注意1进制中任何数值返回都是NaN



拓展延伸：那么如果要将上面的数组解析成正常的10进制数组怎样改变

```shell
['1', '2', '3'].map((item)=>{parseInt(item)})	//可以不穿第二位参数，也可以设置第二位参数为10

//[1,2,3]
```

