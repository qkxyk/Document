### RegExp类型  
创建正则表达式有两种方式：1、字面量形式，2、使用RegExp构造函数。
* 字面量形式  
ECMAScript通过RegExp类型来支持正则表达式。  
```javascript
var expression=/ pattern /flags;
```
其中的模式(pattern)部分可以是任何简单或复杂的正则表达式，可以包含字符类、限定符、分组、向前查找以及反向引用。每个正则表达式都可以带有一或多个标志(flags)，用以标明正则表达式的行为。正则表达式的匹配模式支持以下3个标志。  
1. g:表示全局(global)模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止；
2. i:表示不区分大小写(case-insensitive)模式，即在确定匹配项时忽略模式与字符串的大小写；
3. m:表示多行(multiline)模式，即在到达一行文本末尾时还会继续查找下一行是否存在与模式匹配的项。  
一个正则表达式就时一个模式与上述3个标志位的组合体。不同的组合产生不同的效果。
```javascript
var pattern1=/at/g;//匹配字符串中所有"at"的实例
var pattern2=/[bc]at/i;//匹配第一个"bat"或"cat"，不区分大小写
var pattern3=/.at/gi;//匹配所有以"at"结尾得3个字符组合，不区分大小写
```
与其他语言中的正则表达式类似，模式中使用的所有元字符都必须转义。正则表达式中的元字符包括：
```javascript
( [ { \ ^ $ | ) ? * + . ] }
```  
这些元字符在正则表达式中都有一或多种特殊用途，因此如果想要匹配字符串中包含的这些字符，就必须对它们进行转义。
```javascript
var pattern1=/[bc]at/i;//匹配第一个"bat"或"cat",不区分大小写
var pattern2=/\[bc\]/i;//匹配第一个"[bc]at",不区分大小写
var pattern3=/\.at/gi;//匹配所有".at",不区分大小写
```
* 使用RegExp构造函数  
  >它接收两个参数，一个是要匹配的字符串，另一个是可选的标志字符串。
```javascript
var pattern1=/[bc]at/i;
var pattern2= new RegExp("[bc]at","i");
``` 
上面这两个正则表达式完全等价。不能把正则表达式的字面量传递给RexExp构造函数。由于构造函数的模式参数都是字符串，所以在某些情况下要对字符串进行双重转义，所有的元字符都必须双重转义。例如\n(字符\在字符串中通常被转义为\\,而在正则表达式字符串中就会变成\\\\)。  
使用正则表示字面量和使用RexExp构造函数创建的正则表达式不一样，在ECMAScript 3中，正则表达式字面量始终会共享同一个RegExp实例，而使用构造函数创建的每一个新的RegExp实例都是一个新的实例。在ECMAScript 5中明确规定，使用正则表达式字面量必须像直接条用RegExp构造函数一样，每次都创建新的RegExp实例。
```javascript
var re= null,i;
for(i=0;i<4;i++){
    re=/cat/g;
    var t =re.test("catastronphe");
    console.log(t);
}
for(i=0;i<4;i++){
    re = new RegExp("cat","g");
    var t = re.test("catastronphe");
    console.log(t);
}
```
上面结果在chrome中结果一样(采用ECMAScript 5)  
#### RegExp实例属性  
RegExp的每个实例都有以下属性，通过这些属性可以取得有关模式的各种信息。  
> * global：布尔值，表示是否设置了g标志。
> * ignoreCase:布尔值，表示是否设置了i标志。
> * lastIndex:整数，表示开始搜索下一个匹配项的字符位置，从0开始。
> * multiline：布尔值，表示是否设置了m标志。
> * source：正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。  

通过这些属性可以获知一个正则表达式的各方面信息，但却没有多大用处，因为这些消息全部都包含在模式声明中。
```javascript
var pattern1=/\[bc\]cat/i;
alert(pattern1.source);//"\[bc\]cat"
var pattern2=new RegExp("\\[bc\\]cat","i");
alert(pattern2.source);//"\[bc\]cat"
```  
#### RegExp实例方法  
RegExp对象的主要方法是exec(),该方法时专门为捕获组而设计。exec()接收一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数组，或者再没有匹配项的情况下返回null。返回的数组虽然时Array的实例，但包含两个额外的属性，index和input。其中index表示匹配项在字符串中的位置，而input表示应用正则表达式的的字符串。在数组中，第一项是与整个模式匹配的字符串，其他项是与模式中捕获组匹配的字符串(如果模式中没有捕获组，则该数组只包含以向)。
```javascript
var text='mom and dad and baby';
var pattern=/mom( and dad( and baby)?)?/gi;
var matches=pattern.exec(text);
alert(matches.index);
alert(matches.input);
for(i=0;i<matches.length;i++){
    alert(matches[i]);
};
```

