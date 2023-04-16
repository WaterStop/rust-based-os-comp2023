
> 系列综述：
> 💞目的：本篇文章是个人通过Rustlings学习Rust过程中整理的，整理期间苛求每个知识点，平衡理解简易度与深入程度。
> 🥰来源：材料主要源于`Rustlings`进行的，每个知识点的修正和深入主要参考各平台大佬的文章，其中也可能含有少量的个人实验自证。
> 🤭结语：如果有帮到你的地方，就==点个赞==和==关注一下==呗，谢谢🎈🎄🌷！！！

--- 
 @[TOC]
 
---
**😊[点此到文末惊喜↩︎](#末行锚点)**

---
## <font face="黑体" color=purple>使用前提</font>
1. 配置好rust和vscode环境
2. 进入rustlings的根目录
3. 在命令行输入`rustlings watch`命令，进行自动检测编译模式
4. 按照rustlings环境下命令进行顺序编写，编写完成后删除`// I AM NOT DONE`
6. 每次运行rustlings会进行重新编译，并分析进度和给出错误提示


---
## <font face="黑体" color=purple>Intro</font>
### <font face="黑体" color=purple>Intro.1</font>
1. 答案：啥也不用改，直接删除// I AM NOT DONE即可
2. 知识点
	- 打印宏
	```rust
	// 打印函数
	println!("Hello world");
	```
--- 
### <font face="黑体" color=purple>Intro.2</font>
1. 答案
	```rust
	println!("Hello {}!", "World");
	```
    
2. 知识点
	- `println!`是一个宏
	- 占位符`{}`，会被顺序替换成相应类型的参数
	```rust
	println!("{} World {} {}", "Hello", true, 42);
	//输出结果:
	//Hello World true 42

	let origin = Point { x: 10, y: 20 };
    println!("origin = {}", origin)
	//输出结果：
	//origin = (10, 20)
	```
3. 更多语法可见： [[rust-007]rust的println!函数的各种用法](https://blog.csdn.net/lizhe_dashuju/article/details/108108167)

---
## <font face="黑体" color=purple>Variables</font>
### <font face="黑体" color=purple>基本知识点</font>

1. 变量声明
	- 不可变绑定：`let`将值和变量名进行绑定，声明同时必须初始化
	```rust
	// 不可变绑定
	let x = 5;// 绑定同时必须初始化
	x = 10; // error: 绑定后不能改变
	// 强类型的自动推导
	let x = 1.000;// 编译器会推断为f32
	let x : f64 = 1.000;// 类型注解
	```
	- 可变绑定：使用`mut`表示可变绑定
	```rust
	// 普通的mut可变
	let mut x = 5;
	x = 10;
	```
	- 重新绑定（重影）：变量名称可以被重新使用的机制
	```rust
	// 变量遮蔽的继承可变
	let x = 5; // warning:未使用的符号
	let x = 10;// 可以通过let对同一符号名进行重新绑定
	```
2. 注意：
	- Rust 是`强类型语言`，能类型推导和进行类型安全检查
	- 声明变量最好加`类型注解`，没有注解Rust会进行类型推断，可能不符合预期
	- Rust处于`内存安全`考虑，不允许使用或捕获任何未初始化的变量
	- `位置表达式 = 值表达式`，Rust没有左右值的概念，左边表达式返回内存地址，右边表达式返回值
3. 常量
	- 常量必须加类型，因为局部的类型推断可能出现问题
	- 在编译器进行了类型检查的文本替换，占用代码段或者说不占用内存空间，运行时常量值会被内联到使用的位置
	```rust
	const NUMBER:i32 = 3;
	```
4.  默认不可变的好处
	- 代码逻辑的干净清爽。人们总是默认使用简短的不可变语法，所以使得代码逻辑更加简单
	- 多线程编程中的参数传递。假如语法层面保证了一个值的不可变，就不需要锁保护

---
### <font face="黑体" color=purple>Variables.1</font>
1. 答案：声明一个变量，需要加 let，如果不声明 mut 则默认为不可变变量。
	```rust
	let x = 5;
	println!("x has the value {}", x);
	```
---
### <font face="黑体" color=purple>Variables.2</font>
```rust
    let x: i32 = 10;// 注意初始化类型
    if x == 10 {
        println!("x is ten!");
    } else {
        println!("x is not ten!");
    }

```
---
### <font face="黑体" color=purple>Variables.3</font>
```rust
    let x: i32 = 100;// Rust的变量使用前必须绑定值
    println!("Number {}", x);

```
---
### <font face="黑体" color=purple>Variables.4</font>

```rust
    let mut x = 3;// 可变绑定
    println!("Number {}", x);
    x = 5; // don't change this line
    println!("Number {}", x);

```
---
### <font face="黑体" color=purple>Variables.5</font>
	- const变量的绑定必须要有初始类型和值
```rust
const NUMBER:i32 = 3;
```
---
### <font face="黑体" color=purple>Variables.5</font>

```rust
    let number = "T-H-R-E-E"; // don't change this line
    println!("Spell a Number : {}", number);
    let number = 3; // 重影方式，进行重新绑定
    println!("Number plus two is : {}", number + 2);
```

---
## <font face="黑体" color=purple>Functions</font>
### <font face="黑体" color=purple>Functions.1</font>
这里实际上是对于函数 call_me，有使用但是没有声明，因此我们只需要声明一下即可。

```rust
fn call_me() {

}
```
---
### <font face="黑体" color=purple>Functions.2</font>
函数形参必须指定类型
```rust
fn call_me(num: i32) {
    for i in 0..num {
        println!("Ring! Call number {}", i + 1);
    }
}

```
---
### <font face="黑体" color=purple>Functions.3</font>
函数形参和实参的类型和数量必须匹配

```rust
    call_me(10);
```
---
### <font face="黑体" color=purple>Functions.4</font>
函数返回值使用`->`进行标识
```rust
fn sale_price(price: i32) -> i32{
    if is_even(price) {
        price - 10
    } else {
        price - 3
    }
}

```
---
### <font face="黑体" color=purple>Functions.5</font>
函数的返回值后不需要加分号
```rust
fn square(num: i32) -> i32 {
    num * num
}
```

---
## <font face="黑体" color=purple>if</font>
### <font face="黑体" color=purple>if.1</font>
Rust 的 If statement 部分并不需要加括号
```rust
pub fn bigger(a: i32, b: i32) -> i32 {
    // Complete this function to return the bigger number!
    // Do not use:
    // - another function call
    // - additional variables
    if a > b {
        a
    } else {
        b
    }
}

```

---
### <font face="黑体" color=purple>If.2</font>
这个需要根据下面的测试程序决定没一个输入应该输出什么字符串。
```rust
pub fn foo_if_fizz(fizzish: &str) -> &str {
    if fizzish == "fizz" {
        "foo"
    } else if fizzish == "fuzz" {
        "bar"
    } else {
        "baz"
    }
}
```
---
### <font face="黑体" color=purple>Quiz1</font>
这个小测试实际上需要我们读懂上面的英文含义，并实现calculate_price_of_apples函数。
按照所叙述的要求，当购买数量超过 40 时，每个苹果 1 元，否则 2 元。
```rust
fn calculate_price_of_apples(cnt: i32) -> i32 {
    if cnt <= 40 {
        cnt << 1
    } else {
        cnt
    }
}
```



---
## <font face="黑体" color=purple>Primitive_types</font>
### <font face="黑体" color=purple>Primitive_types.1</font>
可以发现下面的变量 is_evening 有使用没有定义，再考虑到这里代码的语义，可以得到需要填写的代码：

```rust
let is_evening = false; // Finish the rest of this line like the example! Or make it be false!
```

---
### <font face="黑体" color=purple>Primitive_types.2</font>
只需要对于 your_character 这个变量进行定义即可
```rust
let your_character = '3';
```
---
### <font face="黑体" color=purple>Primitive_types.3</font>
定义一个字符串数组，数组里面每一个元素均为 “qaq”，数组总长度为 666.
```rust
let a = ["qaq"; 666];
```
---
### <font face="黑体" color=purple>Primitive_types.4</font>
切片的变量实际上并不能获得地址的所有权的，仅仅是一个引用
```rust
    let nice_slice = &a[1..4];// 前闭后开
```



---
### <font face="黑体" color=purple>Primitive_types.5</font>
元组的使用
```rust
let (name, age) = cat;
```
---
### <font face="黑体" color=purple>Primitive_types.4</font>
获得元组的某一个元素，就直接使用[元组名.index]这样的格式即可。
```rust
let numbers = (1, 2, 3);
 // Replace below ??? with the tuple indexing syntax.
 let second = numbers.1;// 元素的下标引用
 assert_eq!(2, second,
     "This is not the 2nd number in the tuple!")

```




---
## <font face="黑体" color=purple>Vecs</font>
### <font face="黑体" color=purple>Vecs1</font>
使用宏 vec! 来定义一个 vector
```rust
fn array_and_vec() -> ([i32; 4], Vec<i32>) {
    let a = [10, 20, 30, 40]; // a plain array
    let v = vec![10, 20, 30, 40];// TODO: declare your vector here with the macro for vectors
    (a, v)
}
```
---
### <font face="黑体" color=purple>Vecs2</font>
1. 遍历改变 vector 内部元素的方式
	- 迭代器遍历元素
	```rust
	fn vec_loop(mut v: Vec<i32>) -> Vec<i32> {
	   for i in v.iter_mut() {
	       // TODO: Fill this up so that each element in the Vec `v` is
	       // multiplied by 2.
	       *i <<= 1;
	   }
	
	   // At this point, `v` should be equal to [4, 8, 12, 16, 20].
	   v
	}
	```
	-  map 映射：使用匿名函数进行变量的捕获和运算
	```rust
	fn vec_map(v: &Vec<i32>) -> Vec<i32> {
	    v.iter().map(|num| {
	        // TODO: Do the same thing as above - but instead of mutating the
	        // Vec, you can just return the new number!
	        num << 1
	    }).collect()
	}
	
	```


---
## <font face="黑体" color=purple>Move_semantics移动语义</font>
### <font face="黑体" color=purple>基本知识</font>
1. 所有权规则
	- Rust 中的每个值都有一个变量，称为其所有者。
	- 每个值只能有一个所有者，但可以有多个借用者
	- 值所有者的生命周期只在可用范围内，在生命范围结束时，编译器自动调用函数释放资源
3. 变量生命范围
	```rust
	{
	    // 在声明以前，变量 s 无效
	    let s = "runoob";
	    // 这里是变量 s 的可用范围
	}
	// 变量范围已经结束，变量 s 无效
	```
4. 值传递类型
	- 移动语义Move：
		- 引用类型：栈中的指针变量指向堆内存，赋值时使用移动语义，赋值后原指针失效。
	```rust
	let s1 = String::from("hello");
	let s2 = s1;
	// 赋值后s1失效，指向的堆内存所有权移动给s2
	```
	- 拷贝语义Clone：
		- 基本数据类型存在栈中，直接赋值时拷贝语义
	```rust
	let x = 5;
	let y = x;
	// 拷贝语义：赋值后均有效

	// 堆内存的深拷贝
	let s1 = String::from("hello");
    let s2 = s1.clone();
	```
5. 函数参数所有权的传递
	- 在`栈中的基本数据类型`的赋值是`拷贝语义`，在`堆中的引用数据类型`的赋值是`移动语义`
	- `函数返回值的临时变量`可以通过`移动语义`返回到函数调用处
	```rust
	fn main() {
	    let s = String::from("hello");
	    // s 被声明有效
	
	    takes_ownership(s);
	    // s 的值被当作参数传入函数
	    // 所以可以当作 s 已经被移动，从这里开始已经无效
	
	    let x = 5;
	    // x 被声明有效
	
	    makes_copy(x);
	    // x 的值被当作参数传入函数
	    // 但 x 是基本类型，依然有效
	    // 在这里依然可以使用 x 却不能使用 s
	    let s2 = String::from("hello");
		let s3 = takes_and_gives_back(s2);
    	// s2 被当作参数移动, s3 获得返回值所有权
	} // 函数结束, x 无效, 然后是 s. 但 s 已被移动, 所以不用被释放
	
	fn takes_ownership(some_string: String) {
	    // 一个 String 参数 some_string 传入，有效
	    println!("{}", some_string);
	} // 函数结束, 参数 some_string 在这里释放
	
	fn makes_copy(some_integer: i32) {
	    // 一个 i32 参数 some_integer 传入，有效
	    println!("{}", some_integer);
	} // 函数结束, 参数 some_integer 是基本类型, 无需释放
	fn take_and_giveback(a_string:String)->String{
		a_string  // a_string 被当作返回值移出函数
	}
	```
6. 引用
	- 引用是一个指向被引用对象的指针变量，是一种间接访问的方式
	- 引用不会获得值的所有权，引用只能租借（Borrow）值的所有权。
	- 如果被引用对象的所有权发生转移，需要重新租借
	- 不能多重可变引用，为了防止写时碰撞
	- Rust不允许返回局部变量的引用
	```rust
	// 基本引用
	let s1 = String::from("hello");
	let s2 = &s1;
	// 所有权转移引起的租借失效
	let s1 = String::from("hello");
    let mut s2 = &s1;
    let s3 = s1;// s1内存资源所有权转移到s3中，s2的租借失效
    s2 = &s3; // 重新从 s3 租借所有权
    // 可变租借
    let mut s1 = String::from("run");// 被租借对象本身就是可变的
    // s1 是可变的
    let s2 = &mut s1;// 赋予租借者可变的权力
    // s2 是可变的引用
    let s3 = &mut s1;// error，不允许多重可变引用
	```
![在这里插入图片描述](https://img-blog.csdnimg.cn/18f31109f69d4473ae5059b1102ad6bc.png)

---
### <font face="黑体" color=purple>Move_semantics1</font>
vec1 在 11 行进行了修改，而我们在进行变量声明的时候并没有使用 mut 关键字，因此出现错误
```rust
let mut vec1 = fill_vec(vec0);
```

---
### <font face="黑体" color=purple>Move_semantics2</font>
vec0 在进入函数之后，所有权就被传入进去并在函数结束后释放。因此在 fill_vec 之后就再也不能调用 vec0 了。这里解决的方式是通过 clone 的方式进行深拷贝，避免直接使用变量本身。
```rust
let vec0 = Vec::new();
let vec = vec0.clone();
let mut vec1 = fill_vec(vec);
```

---
### <font face="黑体" color=purple>Move_semantics3</font>
问题的核心错误在于函数 fill_vec 的 vec 变量是不可变变量
```rust
fn fill_vec(mut vec: Vec<i32>) -> Vec<i32> {
    vec.push(22);
    vec.push(44);
    vec.push(66);

    vec
}

```

---
### <font face="黑体" color=purple>Move_semantics4</font>
问题：函数调用形参未写，并且局部变量名称相同
```rust
fn fill_vec(vec0: Vec<i32>) -> Vec<i32> {
    let mut vec = vec0;
```
---
### <font face="黑体" color=purple>Move_semantics5</font>
Rust1.31以后，借用的作用域的结束位置从花括号`{}`变成最后一次使用的位置
```rust
fn main() {
    let mut x = 100;
    let y = &mut x;
    *y += 100;// 最后一次使用y，使用完成后会自动释放
    let z = &mut x;
    *z += 1000;
    assert_eq!(x, 1200);
}

```
---
### <font face="黑体" color=purple>Move_semantics6</font>
注释提示了，第一个函数不应该有所有权，第二个函数应该获得所有权。
所以第一个函数使用借用，第二个函数使用移动语义进行直接传递
```rust
fn main() {
    let data = "Rust is great!".to_string();

    get_char(&data);

    string_uppercase(data);
}

// Should not take ownership
fn get_char(data: &String) -> char {// 形参借用也要加&
    data.chars().last().unwrap()
}

// Should take ownership
fn string_uppercase(mut data: String) {
    data = data.to_uppercase();

    println!("{}", data);
}

```













---
## <font face="黑体" color=purple>Structs</font>
### <font face="黑体" color=purple>Structs1</font>
1. 每一个// TODO: 都需要改动
```rust
// 结构的声明方式
struct ColorClassicStruct {
    // TODO: Something goes here
    red: i32,
    green: i32,
    blue: i32,
}
// 元组的声明方式
struct ColorTupleStruct(u8, u8, u8);
// 结构体的初始化及绑定
// TODO: Instantiate a classic c struct!
// let green =
 let green = ColorClassicStruct {
     red: 0,
     green: 255,
     blue: 0,
 };
// 元组的初始化及绑带
let green = ColorTupleStruct(0, 255, 0);
// 实例化一个单元类
let unit_like_struct = UnitLikeStruct;

```
---
### <font face="黑体" color=purple>Structs2</font>
按照断言补足即可
```rust
let your_order = Order {
            name: String::from("Hacker in Rust"),
            year: 2019,
            made_by_phone: false,
            made_by_mobile: false,
            made_by_email: true,
            item_number: 123,
            count: 1,
        };
```

---
### <font face="黑体" color=purple>Structs3</font>
通过断言必须为真，分析代码逻辑，从而改写函数。
```rust
fn is_international(&self) -> bool {
    // Something goes here...
    self.sender_country != self.recipient_country
}

fn get_fees(&self, cents_per_gram: i32) -> i32 {
    // Something goes here...
    self.weight_in_grams * cents_per_gram
}

```

---
## <font face="黑体" color=purple>Enums</font>
### <font face="黑体" color=purple>Enums1</font>
枚举类写法
```rust
enum Message {
    // TODO: define a few types of messages as used below
    Quit,
    Echo,
    Move,
    ChangeColor,
}
```
---
### <font face="黑体" color=purple>Enums2</font>
在枚举类内可以定义不同类型的元素，甚至还可以定义枚举类。
```rust
enum Message {
    // TODO: define the different variants used below
    Move {x: i32, y: i32},
    Echo(String),
    ChangeColor(i32, i32, i32),
    Quit
}
```
---
### <font face="黑体" color=purple>Enums3</font>
match函数和枚举的使用，match类似switch但是不需要break
```rust
// 枚举类
enum Message {
    // TODO: implement the message variant types based on their usage below
    ChangeColor((u8, u8, u8)),
    Echo(String),
    Move(Point),
    Quit,
}
// match函数
match message{
    Message::ChangeColor(t)         =>  self.change_color(t),
    Message::Echo(msg)              => self.echo(msg),
    Message::Move(point)            => self.move_position(point),
    Message::Quit                   => self.quit(), 
};
// 括号？
state.process(Message::ChangeColor((255, 0, 255)));
```


---
## <font face="黑体" color=purple>strings</font>
### <font face="黑体" color=purple>切片相关知识</font>
1. String对象
	- 内存结构：存储在栈上，大小固定为三个字。
		- 一个指向堆中字符串的指针
		- String的容量
		- String的长度
	- 可以根据需要调整容量，通过push_str()追加字符串
	- 保证内部只保存标准的UTF-8文本
2. &str
	- 定义：针对字符串中的特定部分的引用
	- 内存结构：栈上为`切片后字符串在堆的起始地址+长度`，堆上为被引用的字符串
	- 应用场景：常用于作为只读形参
	- 原则：被部分引用的变量不能通过引用进行原值的修改
	- `切片`和`双引号的字符串`都是&str类型
	```rust
	let s = String::from("broadcast");
	let part1 = &s[0..5];// 0，1，2，3，4
	// 参数只读的打印函数
	fn greet(name: &str) {// 类似与const &形参
  		println!("Hello, {}!", name);
	}
	// 切片引用不能修改原值
	let mut s = String::from("runoob");
   	let slice = &s[0..3];
   	s.push_str("yes!"); // 错误
	```
3. String和&str的转换
	- String 和 str 都支持切片，切片的结果是 &str 类型的数据。
	```rust
	
	let s1 = String::from("hello");
	let s2 = &s1[..];// String 转换成 &str
	let s3 = s2.tostring();
	```
4. 切片（Slice）是对数据值的部分引用。切片变量实际为`片开始指针 + 大小`
![在这里插入图片描述](https://img-blog.csdnimg.cn/b88ceaf7e017410c821809456e88d1dd.png)
7. 范围运算符`..`，其中x..y 表示 [x, y) 的数学含义
	```rust
	..y 	// 等价于 0..y
	x.. 	// 等价于位置 x 到数据结束
	.. 		// 等价于位置 0 到结束
	x..y	// x到y前闭后开
	```
9. 其他线性数据结构也支持切片操作，例如数组
	```rust
	let arr = [1, 3, 5, 7, 9];
    let part = &arr[0..3];
    for i in part.iter() {
        println!("{}", i);
    }
	```### <font face="黑体" color=purple>strings.1</font>

---
### <font face="黑体" color=purple>strings1</font>
简单的&str转换成String对象
```rust
fn current_favorite_color() -> String {
    "blue".to_string()
}
```
---
### <font face="黑体" color=purple>strings2</font>
参数类型的更改
```rust
fn is_a_color_word(attempt: String) -> bool {
    attempt == "green" || attempt == "blue" || attempt == "red"
}
```

---
### <font face="黑体" color=purple>strings3</font>
注释已经标出
```rust

fn trim_me(input: &str) -> String {
    // TODO: Remove whitespace from both ends of a string!
    input.trim().to_string() // trim()除了单词间的空格全部消除
}

fn compose_me(input: &str) -> String {
    // TODO: Add " world!" to the string! There's multiple ways to do this!
    format!("{} world!", input) // 审题
}

fn replace_me(input: &str) -> String {
    // TODO: Replace "cars" in the string with "balloons"!
    input.replace("cars", "balloons") // 替换单词
}

```

---
### <font face="黑体" color=purple>strings4</font>
根据第一个小标题下的切片知识可以做出来
```rust
fn main() {
    string_slice("blue");
    string("red".to_string());
    string(String::from("hi"));
    string_slice("rust is fun!".to_owned());
    string_slice("nice weather".into());
    string_slice(format!("Interpolation {}", "Station"));
    string_slice(&String::from("abc")[0..1]);
    string_slice("  hello there ".trim());
    string("Happy Monday!".to_string().replace("Mon", "Tues"));
    string_slice("mY sHiFt KeY iS sTiCkY".to_lowercase());
}
```




---
## <font face="黑体" color=purple>Modules</font>
### <font face="黑体" color=purple>Modules1</font>
在外面使用，因此需要定义为pub
```rust
pub fn make_sausage() {
        get_secret_recipe();
        println!("sausage!");
    }
```
---
### <font face="黑体" color=purple>Modules2</font>
给模块起别名，注意末尾的分号，并且外界需要使用就加pub
```rust
pub use self::fruits::PEAR as fruit;
pub use self::veggies::CUCUMBER as veggie;
```

---
### <font face="黑体" color=purple>Modules3</font>
使用 use 关键字来引入标准库
```rust
use std::time::{SystemTime, UNIX_EPOCH};
```


---
## <font face="黑体" color=purple>Hashmaps</font>
### <font face="黑体" color=purple>Hashmaps1</font>
哈希表的定义
```rust
let mut basket = HashMap::new();
```
哈希表的插入
```rust
basket.insert(String::from("apple"), 1);
basket.insert(String::from("mango"), 2);
```
---
### <font face="黑体" color=purple>Hashmaps2</font>
通过 entry 获取得到针对某个字符的记录，or_insert在哈希表中检查条目中是否已经存在参数值，没有则插入
```rust
basket.entry(fruit).or_insert(1);
```

---
### <font face="黑体" color=purple>Hashmaps3</font>
与上题相同，但需要逻辑判断
```rust
let score = scores.entry(team_1_name.clone()).or_insert(Team {
            name: team_1_name,
            goals_scored: 0,
            goals_conceded: 0,
        });
(*score).goals_scored += team_1_score;
(*score).goals_conceded += team_2_score;
let score = scores.entry(team_2_name.clone()).or_insert(Team {
    name: team_2_name,
    goals_scored: 0,
    goals_conceded: 0,
});
(*score).goals_scored += team_2_score;
(*score).goals_conceded += team_1_score;
```

---
### <font face="黑体" color=purple>quiz2</font>
```rust
mod my_module {
    use super::Command;

    // TODO: Complete the function signature!
    pub fn transformer(input: Vec<(String, Command)>) -> Vec<String> {
        // TODO: Complete the output declaration!
        let mut output: Vec<String> = vec![];
        for (string, command) in input.iter() {
            // TODO: Complete the function body. You can do it!
            match command {
                Command::Uppercase => {
                    output.push(string.to_uppercase());
                }
                Command::Trim => {
                    output.push(string.trim().to_string());
                }
                Command::Append(usize) => {
                    let mut ans = String::new();
                    for i in 0..*usize {
                        ans += &string.clone();
                    }
                    output.push(format!("{}bar", ans));
                }
            }
        }
        output
    }
}

```
网上答案可能不行，因为从github上clone下来的项目中的路径配置与本地不同，可能导致相对路径失效，需要使用绝对路径
```rust
  // TODO: What do we have to import to have `transformer` in scope?
    use crate::my_module::transformer;
```



---
## <font face="黑体" color=purple>Options</font>
### <font face="黑体" color=purple>基础知识</font>

1. 目的：避免出现程序员忘记检查null和none的问题
2. 用法：
	- 返回值要么是`Some(Vaule)`，要么是`None`
3. Option和Result是枚举(Enum)类型, 枚举的特点是:
	- 同一时间只能存在一个枚举值, 对应非黑即白的`独一性`
	- 枚举可以把不相干的任意类型组合进行`强制打包`
	- 在使用match/ if let 等判断语法时候, 必须穷尽一切可能性(或者隐性穷尽, 比如你只需要处理Some的情况) , 对应必须判断这个值是Some 还是None


---
### <font face="黑体" color=purple>Options1</font>
按要求返回值，并且在判断时需要进行Some的包含
```rust
if time_of_day > 24 {
        None
    } else if time_of_day >= 22 {
        Some(0)
    } else {
        Some(5)
    }
    
#[test]
fn raw_value() {
    // TODO: Fix this test. How do you get at the value contained in the Option?
    let icecreams = maybe_icecream(12);
    assert_eq!(icecreams, Some(5));
}
```
---
### <font face="黑体" color=purple>Options2</font>
这里需要两层 Some 的原因是因为 Vec 的 pop 函数会套一层 Option<T>.
```rust
if let Some(word) = optional_target {
	assert_eq!(word, target);
}
while let Some(Some(integer)) = optional_integers.pop() {
    assert_eq!(integer, range);
    range -= 1;
}

```
---
### <font face="黑体" color=purple>Options3</font>
这里是需要让 match 语句不拥有所有权，而是采用借用的方式，采用 ref 关键字。
```rust
    match y {
        Some(p) => println!("Co-ordinates are {},{} ", p.x, p.y),
        _ => println!("no match"),
    }
```
---


---
## <font face="黑体" color=purple>error_handling</font>
### <font face="黑体" color=purple>基础知识</font>

1. 异常判断是一个枚举类
```rust
enum Result<type(T), type(E)> {
    Ok(T),
    Err(E),
}

// 使用
if name.is_empty() {
   // Empty names aren't allowed.
    Err("`name` was empty; it must be nonempty.".to_string())
} else {
    Ok(format!("Hi! My name is {}", name))
}
```
2. `?操作符`
	- 只能使用在以Option或者Result作为返回值的函数体中。
```rust
let result :Result<T,E1> = ···;
// ？操作符的使用
let ok = result?;
ok;
// 上面语句的去糖展开式
let ok = match result{
	OK(ok) => ok,// 成功则内部值T和作为表达式的返回结果
	Err(err)=>return Err(From::from(err))// 失败则将操作符前的E1转换类型为Result<T, E2>中的E2并返回
};
```
3. DST(Dynamically sized types) 是rust里一项非常有用的特性，结合trait object动态派发，在性能开销很小的情况下实现了更灵活的编码
4. Rust中的调用分配类型
	- 静态派发：在编译期完成
	- 动态派发：将函数的选定和调用延迟到运行时
5. 组合器
	- 通过各种方式组合T类型的值以建立更复杂的T类型的值
	- 使用组合器自动化地构造很多所需的程序，而不是手工编写每个细节。
6. 组合器的使用
	- or()和and()组合两个返回值为Option/Result的表达式
		- or()：如果其中一个得到了Some或Ok，该值将立即返回。
		- and()：如果两个都获得Some或Ok，则返回第二个表达式的值。如果其中一个为None或Err，则该值立即返回。
	```rust
	fn main() {
		let s1 = Some("some1");
		let s2 = Some("some2");
		let n: Option<&str> = None;
	​
		let o1: Result<&str, &str> = Ok("ok1");
		let o2: Result<&str, &str> = Ok("ok2");
		let e1: Result<&str, &str> = Err("error1");
		let e2: Result<&str, &str> = Err("error2");
		​
		assert_eq!(s1.or(s2), s1); // Some1 or Some2 = Some1
		assert_eq!(s1.or(n), s1);  // Some or None = Some
		assert_eq!(n.or(s1), s1);  // None or Some = Some
		assert_eq!(n.or(n), n);    // None1 or None2 = None2
		
		assert_eq!(s1.and(s2), s2); // Some1 and Some2 = Some2
		assert_eq!(s1.and(n), n);   // Some and None = None
		assert_eq!(n.and(s1), n);   // None and Some = None
		assert_eq!(n.and(n), n);    // None1 and None2 = None1
	```
	- map() and map_err()：Rust也提供了map()作为迭代器的适配器，以便在迭代器的每个元素上应用闭包，以将其转换为另一个迭代器。
		- map()：通过应用闭包转换类型T。 Some或Ok块的数据类型可以根据闭包的返回类型进行更改。将Option<T>转换为Option<U>，Result<T, E>转换为Result <U, E>
		- Result类型的map_err()：可以根据闭包的返回类型来更改Err块的数据类型。将Result <T, E>转换为Result <T, F>。
	```rust
	// 类型映射
	let s1 = Some("abcde");
	let s2 = Some(5);
	let fn_character_count = |s: &str| s.chars().count();
	let fn_character_count = |s: &str| s.chars().count();
	// map_err()，只有Err值被改变
	let o1: Result<&str, &str> = Ok("abcde");
	let o2: Result<&str, isize> = Ok("abcde");
	let fn_character_count = |s: &str| -> isize { s.parse().unwrap() }; // convert str to isize
	​assert_eq!(o1.map_err(fn_character_count), o2); // Ok1 map = Ok2
	```





---
### <font face="黑体" color=purple>error1</font>

```rust
pub fn generate_nametag_text(name: String) -> Result<String, String> {
    if name.is_empty() {
        // Empty names aren't allowed.
        Err("`name` was empty; it must be nonempty.".to_string())
    } else {
        Ok(format!("Hi! My name is {}", name))
    }
}
```


---
### <font face="黑体" color=purple>error2</font>
详情见本节基础知识2
```rust
let qty = item_quantity.parse::<i32>()?;
```
---
### <font face="黑体" color=purple>error3</font>
`？操作符`只能用于返回类型为`Result<T, E1> `的函数
```rust
fn main() -> Result<(), ParseIntError> {
    let mut tokens = 100;
    let pretend_user_input = "8";
    let cost = total_cost(pretend_user_input)?;
    if cost > tokens {
        println!("You can't afford that many!");
    } else {
        tokens -= cost;
        println!("You now have {} tokens.", tokens);
    }
    Ok(())
}
```
---
### <font face="黑体" color=purple>error4</font>
有对要有错，除了使用？操作符，进行隐式的错误类型转换返回
```rust
fn new(value: i64) -> Result<PositiveNonzeroInteger, CreationError> {
    // Hmm...? Why is this only returning an Ok value?
    if value < 0 {
        return Err(CreationError::Negative);
    } else if value == 0 {
        return Err(CreationError::Zero);
    }
    Ok(PositiveNonzeroInteger(value as u64))
}
```

---
### <font face="黑体" color=purple>error5</font>
box作为智能指针可以用于解决编译时大小未知的问题
```rust
fn main() -> Result<(), Box<dyn error::Error>> {
    let pretend_user_input = "42";
    let x: i64 = pretend_user_input.parse()?;
    println!("output={:?}", PositiveNonzeroInteger::new(x)?);
    Ok(())
}
```

---
### <font face="黑体" color=purple>error6</font>
这里是需要让 match 语句不拥有所有权，而是采用借用的方式，采用 ref 关键字。
```rust
fn from_parseint(err: ParseIntError) -> ParsePosNonzeroError {
    ParsePosNonzeroError::ParseInt(err)
}
// 
let x: i64 = s.parse().map_err(ParsePosNonzeroError::from_parseint)?;
PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)
```










---

## <font face="黑体" color=purple>generics</font>
### <font face="黑体" color=purple>基础知识</font>

---
### <font face="黑体" color=purple>generics1</font>
占用符：使编译器自己进行推断类型，类似auto?

```rust
let mut shopping_list: Vec<_> = Vec::new();
```
---
### <font face="黑体" color=purple>generics2</font>
模板类的使用
```rust

struct Wrapper<T> {
    value: T,
}

impl<T> Wrapper<T>{
    pub fn new(value: T) -> Self {
        Wrapper { value }
    }
}
```

---
## <font face="黑体" color=purple>traits</font>
### <font face="黑体" color=purple>基础知识</font>
1. Trait是对一组抽象接口的描述
	- 所有的Trait都定义了一个隐含类型Self，其指向实现该Trait的类型
	- 组成
		- functions（方法）
		- types（类型）
		- constants（常量）
	- Self和self
		- Self：实现Trait的类型的别名
		- self：方法参数 fn f(self) {}，等价于fn f(self: Self) {}
```rust
// 接口
 trait Hello {
     fn say_hi(&self) {
         println!("hi");
     }
 }
 ​
 struct Student {}
 impl Hello for Student {}// 给类添加接口
 struct Teacher {}
impl Hello for Teacher {// 接口的重写Override
     fn say_hi(&self) {
         println!("hi, I'm teacher Lee.");
     }
 }
 ​
 fn main() {
     let s = Student {};
     s.say_hi();
     let t = Teacher {};
     t.say_hi();
 }
```

---
### <font face="黑体" color=purple>traits1</font>
注释提示了，第一个函数不应该有所有权，第二个函数应该获得所有权。
所以第一个函数使用借用，第二个函数使用移动语义进行直接传递
```rust
impl AppendBar for String {
    // TODO: Implement `AppendBar` for type `String`.
    fn append_bar(self) -> Self {
        format!("{}{}", self, "Bar")
    }
}
```

---
### <font face="黑体" color=purple>traits2</font>
注释提示了，第一个函数不应该有所有权，第二个函数应该获得所有权。
所以第一个函数使用借用，第二个函数使用移动语义进行直接传递
```rust

impl AppendBar for Vec<String>
{
    fn append_bar(mut self) -> Self
    {
            self.push("Bar".to_string());
            self
    }
}
```

---
### <font face="黑体" color=purple>traits3</font>
```rust
pub trait Licensed {
    fn licensing_info(&self) -> String {
        String::from("Some information")
    }
}
```
---
### <font face="黑体" color=purple>traits4</font>
类对象类型
```rust
fn compare_license_types(software: impl Licensed, software_two: impl Licensed) -> bool {
    software.licensing_info() == software_two.licensing_info()
}
```

---
## <font face="黑体" color=purple>test</font>
### <font face="黑体" color=purple>test1</font>
简单的assert判断
```rust
#[cfg(test)]
mod tests {
    #[test]
    fn you_can_assert() {
        assert!(true);
    }
}
```

---
### <font face="黑体" color=purple>test2</font>
注释提示了，第一个函数不应该有所有权，第二个函数应该获得所有权。
所以第一个函数使用借用，第二个函数使用移动语义进行直接传递
```rust
#[cfg(test)]
mod tests {
    #[test]
    fn you_can_assert_eq() {
        assert_eq!("a", "a");
    }
}
```

---
### <font face="黑体" color=purple>test3</font>
```rust
#[test]
fn is_true_when_even() {
    assert!(is_even(90));
}

#[test]
fn is_false_when_odd() {
    assert!(is_even(92));
}
```
---
### <font face="黑体" color=purple>quiz3</font>
类对象类型
```rust
pub struct ReportCard<T> {// 泛型
    pub grade: T, 
    pub student_name: String,
    pub student_age: u8,
}

impl<T: std::fmt::Display> ReportCard<T> {// std::fmt::Display用于异常显示的自定义
    pub fn print(&self) -> String {
        format!(
            "{} ({}) - achieved a grade of {}",
            &self.student_name, &self.student_age, &self.grade
        )
    }
}

#[test]
fn generate_alphabetic_report_card() {
    // TODO: Make sure to change the grade here after you finish the exercise.
    let report_card = ReportCard {
        grade: "A+", // 根据assert进行修改
        student_name: "Gary Plotter".to_string(),
        student_age: 11,
    };
    assert_eq!(
        report_card.print(),
        "Gary Plotter (11) - achieved a grade of A+"
    );
}

```



---
## <font face="黑体" color=purple>lifetimes</font>
### <font face="黑体" color=purple>基础知识</font>
1. 函数生命周期
	- 原因：编译器有时无法静态推断函数中形参和返回值的生命周期，需要显式声明参数的生命周期。
	- 目标：防止悬空指针
	- 规则：同名生命周期参数绑定的对象，
```rust
// 隐式生命周期
// 编译器在编译时无法推导出返回值，只有运行时才能推导出来
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}

// 显式生命周期
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
//当编译器看到x: &'a str的时候，'a会被编译器推断为x的生命周期
//当编译器看到y: &'a str的时候，编译器会将'a推断为y的生命周期
//但是此时有冲突，于是编译器会将'a推断为x和y的生命周期中最小的那个。
```
2. struct生命周期
	- 当一个生命周期参数修饰多个字段的时候，编译器会将这个生命周期参数推断出这几个字段生命周期最小的那个。
	```rust
	struct Foo<'a, 'b> {
	    x: &'a i32,
	    y: &'b i32,
	}
	
	fn main() {
	
	    let x = 6;
	    let m;                     
	// x和y生命周期相同，打印时已经失效
	    {                          
	        let y = 6;            
	        let f = Foo { x: &x, y: &y };  
	        m = f.x;             
	    }                          
	
	    println!("{}", m);        
	}
	```
3. 省略生命周期声明
	- 函数的每个参数将会赋予各自的生命周期。例如fn foo(x: &i32)将相当于为fn foo<'a>(x: &'a i32)，fn foo(x: &i32, y: &i32)相当于fn foo<'a, 'b>(x: &'a i32, y: &'b i32)，以此类推。
	- 如果输入参数只有一个生命周期参数，那个这个生命周期参数将会被赋予所有输入值。例如fn foo(x: &i32) -> &i32相当于fn foo<'a>(x: &'a i32) -> &'a i32。
	- 在struct的impl语句中，如果有多个输入参数，但是输入参数中有&self或者&mut self，那么self的生命周期将会被赋予所有的书参数。这条规则对于编写struct方法是非常有利的。

---
### <font face="黑体" color=purple>lifetimes1</font>
当一个生命周期参数修饰多个字段的时候，编译器会将这个生命周期参数推断出这几个字段生命周期最小的那个。
```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

---
### <font face="黑体" color=purple>lifetimes2</font>
result被绑定后，在括号时被释放
```rust
fn main() {
    let string1 = String::from("long string is long");
    let result;
    {
        let string2 = String::from("xyz");
        result = longest(string1.as_str(), string2.as_str());
        println!("The longest string is '{}'", result);
    }
}
```

---
### <font face="黑体" color=purple>lifetimes3</font>
```rust
struct Book<'a, 'b> {
    author: &'a str,
    title: &'b str,
}
```



---
## <font face="黑体" color=purple>iterators</font>
### <font face="黑体" color=purple>基础知识</font>
1. 迭代器类型
	- iter返回的是`值的不可变引用`，即&T
	- iter_mut返回的是`值的可变引用`，即&mut T
	- into_iter返回的是`值的所有权`T类型的值

---
### <font face="黑体" color=purple>iterators1</font>
值的不可变引用
```rust

let mut my_iterable_fav_fruits = my_fav_fruits.iter();   // TODO: Step 1

 assert_eq!(my_iterable_fav_fruits.next(), Some(&"banana"));
 assert_eq!(my_iterable_fav_fruits.next(), Some(&"custard apple"));     // TODO: Step 2
 assert_eq!(my_iterable_fav_fruits.next(), Some(&"avocado"));
 assert_eq!(my_iterable_fav_fruits.next(), Some(&"peach"));     // TODO: Step 3
 assert_eq!(my_iterable_fav_fruits.next(), Some(&"raspberry"));
 assert_eq!(my_iterable_fav_fruits.next(), None);     // TODO: Step 4
```

---
### <font face="黑体" color=purple>iterators2</font>
```rust
// to_uppercase函数：返回字符串的大写字母
// collect函数：将一个集合的内容移动到另一个集合的主要方式
// as_str() 可以显式提取包含该字符串的字符串片段
// next函数会让迭代器指向下一个对象
pub fn capitalize_first(input: &str) -> String {
    let mut c = input.chars();
    match c.next() {
        None => String::new(),
        Some(first) => first.to_uppercase().collect::<String>() + c.as_str(),的大写字母
    }
}

// 改变vector中第一个字母为大写字母
pub fn capitalize_words_vector(words: &[&str]) -> Vec<String> {
    let mut col = vec![];
    for word in words
    {
        col.push(capitalize_first(word));
    }
    col 
}

//.join(" ") 将多维数组降维成中间为空格的一维数组
pub fn capitalize_words_string(words: &[&str]) -> String {
    let mut buffer = vec![];
    for word in words {
        buffer.push(capitalize_first(word));
        //println!("{:?}", buffer);
    }

    buffer.join("")
}
```

---
### <font face="黑体" color=purple>iterators3</font>
组合器的拆分
```rust
// Calculate `a` divided by `b` if `a` is evenly divisible by `b`.
// Otherwise, return a suitable error.
pub fn divide(a: i32, b: i32) -> Result<i32, DivisionError> {
    if b == 0 {
        return Err(DivisionError::DivideByZero);
    } else if a % b == 0 {
        Ok(a / b)
    } else {
        return Err(DivisionError::NotDivisible(NotDivisibleError {
            dividend: a,
            divisor: b,
        }));
    }
}

// Complete the function and return a value of the correct type so the test passes.
// Desired output: Ok([1, 11, 1426, 3])
fn result_with_list() -> Result<Vec<i32>, DivisionError> {
    let numbers = vec![27, 297, 38502, 81];
    //let division_results = numbers.into_iter().map(|n| divide(n, 27));
    let mut buf = Vec::<i32>::new();
    for n in numbers {
        match divide(n, 27) {
            Ok(r) => buf.push(r),
            Err(e) => return Err(e),
        }
    }

    Ok(buf)
}

// Complete the function and return a value of the correct type so the test passes.
// Desired output: [Ok(1), Ok(11), Ok(1426), Ok(3)]
fn list_of_results() -> Vec<Result<i32, DivisionError>> {
    let numbers = vec![27, 297, 38502, 81];
    //let division_results = numbers.into_iter().map(|n| divide(n, 27));
    let mut buf = Vec::new();

    for n in numbers {
        match divide(n, 27) {
            Ok(r) => buf.push(Ok(r)),
            Err(e) => buf.push(Err(e)),
        }
    }
    buf
}
```

---
### <font face="黑体" color=purple>iterators4</font>
```rust
pub fn factorial(num: u64) -> u64 {
    (1..=num).product()// 表示1到num中所有的数字的乘积
}
```
---
### <font face="黑体" color=purple>iterators5</font>

```rust
// iter()获取map的迭代器
// filter()HashMap中第一个元素value相等的值
// count()用来返回数量
fn count_iterator(map: &HashMap<String, Progress>, value: Progress) -> usize {
    // map is a hashmap with String keys and Progress values.
    // map = { "variables1": Complete, "from_str": None, ... }
    let count = map.iter().filter(|v| *v.1 == value).count();
    count
}

fn count_collection_iterator(collection: &[HashMap<String, Progress>], value: Progress) -> usize {
    // collection is a slice of hashmaps.
    // collection = [{ "variables1": Complete, "from_str": None, ... },
    //     { "variables2": Complete, ... }, ... ]
    let mut my_map1 = collection[0].clone();
    let mut my_map2 = collection[1].clone();
	// 调用extend方法，将my_map1转换为一个迭代器，并将其键值对添加到my_map2中
    my_map2.extend(my_map1.into_iter());
	// 与上一个相同
    let count11 = my_map2
        .iter()
        .filter(|v| *v.1 == Progress::Complete)
        .count();
    count11
}
```

---
## <font face="黑体" color=purple>threads</font>
### <font face="黑体" color=purple>基本知识</font>
1. 进程是资源分配的最小单位，而线程是CPU调度的最小单位。即同一个进程下会有多个线程同时存在，这些线程共同使用一套映射表。
2. 实现了同一个进程下的两个线程(main线程和spawn线程)
	- main线程执行完毕后会将子线程强制终止：通过join方法解决
	```rust
	use std::thread;
	use std::time::Duration;
	
	fn main() {
	    let handle = thread::spawn(||{
	        //创建一个子线程
	        for i in 1..10 {
	            println!("number {} in spawn thread!",i);
	            thread::sleep(Duration::from_millis(1));
	            //规定输出后的睡眠时间
	        }
	    });
		
		//handle.join().unwrap();
    	//如果将join()设置在这里，则会先进行子线程，等待子线程结束后才会进入主线程执行任务
		
	    for j in 1..5 {
	        //这里是主线程的任务
	        println!("number {} in main thread!",j);
	        thread::sleep(Duration::from_millis(1));
	    }
	    println!("main thread end!");
	    handle.join().unwrap();
	    //通过join()让主线程结束后等待子线程结束
	    //如果不设置，则主线程结束后自动中断子线程
	}
	```
3. 变量所有权问题
	- 关键字move：在闭包中，强制获取环境变量的所有权。防止获取的内存引用失效。
	- 闭包使用了move，则将v的所有权转移给了闭包，此时是无法在main作用域中再次使用v的
	```rust
	use std::thread;
	//use std::time::Duration;
	
	fn main() {
	    let v = vec![1,2,3];
	
	    let handle = thread::spawn(move ||{
	        println!("{:?}",v);
	    });
	
	    handle.join().unwrap();
	
	    println!("Hello, world!");
	}
	
	
	```

---
### <font face="黑体" color=purple>threads1</font>
创建了10个线程，每个线程睡眠250毫秒，然后打印自己的编号和耗时
使用JoinHandle的join方法来等待每个线程结束，并获取它们的返回值
```rust
for handle in handles {
	let result = handle.join().unwrap();
    results.push(result);
}
```

---
### <font face="黑体" color=purple>threads2</font>
unwrap函数：计算结果，如果有错误，painc并停止程序
```rust
use std::sync::{Arc, Mutex};// 需要使用互斥
use std::thread;
use std::time::Duration;

struct JobStatus {
    jobs_completed: u32,
}

fn main() {
    let status = Arc::new(Mutex::new(JobStatus { jobs_completed: 0 }));// 声明互斥对象
    let mut handles = vec![];
    for _ in 0..10 {
        let status_shared = status.clone();// 拷贝对象
        let handle = thread::spawn(move || {
            thread::sleep(Duration::from_millis(250));
            // TODO: You must take an action before you update a shared value
            status_shared.lock().unwrap().jobs_completed += 1;
        });
        handles.push(handle);
    }
    for handle in handles {
        handle.join().unwrap();
        // TODO: Print the value of the JobStatus.jobs_completed. Did you notice anything
        // interesting in the output? Do you have to 'join' on all the handles?
        println!("jobs completed {}", status.lock().unwrap().jobs_completed);
    }
}
```

---
### <font face="黑体" color=purple>threads3</font>
```rust
#[test]
fn is_true_when_even() {
    assert!(is_even(90));
}

#[test]
fn is_false_when_odd() {
    assert!(is_even(92));
}
```



---
## <font face="黑体" color=purple>smart_pointers</font>
### <font face="黑体" color=purple>box1</font>
Box<T> 类型是一个智能指针，它允许 Box<T> 值被当作引用对待
有详细解释https://www.rustwiki.org.cn/zh-CN/book/ch15-01-box.html?highlight=box#%E4%BD%BF%E7%94%A8-boxt-%E6%8C%87%E5%90%91%E5%A0%86%E4%B8%8A%E7%9A%84%E6%95%B0%E6%8D%AE
```rust
pub enum List {
    Cons(i32, Box<List>),// Box将值放在堆上，而不是栈上
    Nil,
}


pub fn create_empty_list() -> List {
    List::Nil
}

pub fn create_non_empty_list() -> List {
    List::Cons(0, Box::new(List::Nil))
}
```

---
### <font face="黑体" color=purple>rc1</font>
Box<T> 自定义了 Drop 用来释放 box 所指向的堆空间。
Rc<T> 记录了堆上数据的引用数量以便可以拥有多个所有者
```rust
// TODO
let saturn = Planet::Saturn(Rc::clone(&sun));
println!("reference count = {}", Rc::strong_count(&sun)); // 7 references
saturn.details();

// TODO
let uranus = Planet::Uranus(Rc::clone(&sun));
println!("reference count = {}", Rc::strong_count(&sun)); // 8 references
uranus.details();

// TODO
let neptune = Planet::Neptune(Rc::clone(&sun));
println!("reference count = {}", Rc::strong_count(&sun)); // 9 references
neptune.details();

// TODO
drop(earth);
println!("reference count = {}", Rc::strong_count(&sun)); // 3 references

// TODO
drop(venus);
println!("reference count = {}", Rc::strong_count(&sun)); // 2 references

// TODO
drop(mercury);
println!("reference count = {}", Rc::strong_count(&sun)); // 1 reference

```

---
### <font face="黑体" color=purple>arc1</font>
原子引用计数 Arc<T>，但是原子性的使用会带来性能的降低
```rust
let shared_numbers = Arc::new(numbers);// TODO
let child_numbers = Arc::clone(&shared_numbers);// TODO
```

---
### <font face="黑体" color=purple>cow1</font>
1.  Clone-On-Write，即在写入时进行克隆操作。Cow 类型可以用来避免不必要的内存分配和复制操作，从而提高程序的性能和效率
2. 作用
	- 读写分离：在一些业务场景中，需要对某个数据结构进行多次读取和少量修改，但是每次修改都会导致内存分配和复制操作，从而影响程序的性能和效率。Cow 类型可以通过克隆操作来避免这个问题，从而提高程序的性能和效率。
	- 借用检查：在 Rust 中，借用检查是一项重要的安全特性，可以避免程序中出现内存安全问题。但是，在某些情况下，借用检查会导致代码的复杂度和可读性变差。Cow 类型可以通过引用和克隆操作来解决这个问题，从而简化代码的实现和维护。
```rust
// TODO
Cow::Borrowed(_) => Ok(()),
_ => panic!("expected borrowed value"),

// TODO
Cow::Owned(_) => Ok(()),
_ => panic!("expected owned value"),

// TODO
Cow::Owned(_) => Ok(()),
_ => panic!("expected borrowed value"),

```





---
## <font face="黑体" color=purple>smart_pointers</font>
### <font face="黑体" color=purple>box1</font>
Box<T> 类型是一个智能指针，它允许 Box<T> 值被当作引用对待
有详细解释https://www.rustwiki.org.cn/zh-CN/book/ch15-01-box.html?highlight=box#%E4%BD%BF%E7%94%A8-boxt-%E6%8C%87%E5%90%91%E5%A0%86%E4%B8%8A%E7%9A%84%E6%95%B0%E6%8D%AE
```rust
pub enum List {
    Cons(i32, Box<List>),// Box将值放在堆上，而不是栈上
    Nil,
}


pub fn create_empty_list() -> List {
    List::Nil
}

pub fn create_non_empty_list() -> List {
    List::Cons(0, Box::new(List::Nil))
}
```

---
### <font face="黑体" color=purple>rc1</font>
Box<T> 自定义了 Drop 用来释放 box 所指向的堆空间。
Rc<T> 记录了堆上数据的引用数量以便可以拥有多个所有者
```rust
// TODO
let saturn = Planet::Saturn(Rc::clone(&sun));
println!("reference count = {}", Rc::strong_count(&sun)); // 7 references
saturn.details();

// TODO
let uranus = Planet::Uranus(Rc::clone(&sun));
println!("reference count = {}", Rc::strong_count(&sun)); // 8 references
uranus.details();

// TODO
let neptune = Planet::Neptune(Rc::clone(&sun));
println!("reference count = {}", Rc::strong_count(&sun)); // 9 references
neptune.details();

// TODO
drop(earth);
println!("reference count = {}", Rc::strong_count(&sun)); // 3 references

// TODO
drop(venus);
println!("reference count = {}", Rc::strong_count(&sun)); // 2 references

// TODO
drop(mercury);
println!("reference count = {}", Rc::strong_count(&sun)); // 1 reference

```

---
### <font face="黑体" color=purple>arc1</font>
原子引用计数 Arc<T>，但是原子性的使用会带来性能的降低
```rust
let shared_numbers = Arc::new(numbers);// TODO
let child_numbers = Arc::clone(&shared_numbers);// TODO
```






---
## <font face="黑体" color=purple>macros</font>
### <font face="黑体" color=purple>macros1</font>
宏调用需要加！
```rust
my_macro!();
```

---
### <font face="黑体" color=purple>macros2</font>
宏先声明后使用

---
### <font face="黑体" color=purple>macros3</font>
宏模块需要声明
```rust
#[macro_use]
mod macros {
    macro_rules! my_macro {
        () => {
            println!("Check out my macro!");
        };
    }
}
```

---
### <font face="黑体" color=purple>macros4</font>
删除`#[rustfmt::skip]`，Rustfmt 会遍历 mod 树，将该属性放在声明要忽略的模块的文件

---
## <font face="黑体" color=purple>clippy</font>

### <font face="黑体" color=purple>clippy1</font>
1. clippy 工具是一系列 lint 的集合，用于捕捉常见错误和改进 Rust 代码
```rust
//let pi = 3.14f32;
let radius = 5.00f32;

let area = f32::consts::PI * f32::powi(radius, 2);
```

---
### <font face="黑体" color=purple>clippy2</font>
```rust
if let Some(x) = option {
        res += x;
    }

```

---
### <font face="黑体" color=purple>clippy3</font>
```rust

#[allow(unused_variables, unused_assignments)]
fn main() {
    let my_option: Option<()> = None;
    if my_option.is_none() {
        //my_option.unwrap();
    }

    let my_arr = &[-1, -2, -3 - 4, -5, -6];
    println!("My array! Here it is: {:?}", my_arr);

    let mut my_empty_vec = vec![1, 2, 3, 4, 5];
    my_empty_vec.clear();
    println!("This Vec is empty, see? {:?}", my_empty_vec);

    let mut value_a = 45;
    let mut value_b = 66;
    // Let's swap these two!
    std::mem::swap(&mut value_a, &mut value_b);

    println!("value a: {}; value b: {}", value_a, value_b);
}
```



---
## <font face="黑体" color=purple>conversions</font>

### <font face="黑体" color=purple>using_as</font>
类型转换
```rust
total / values.len() as f64
```

---
### <font face="黑体" color=purple>from_into</font>
```rust
impl From<&str> for Person {
    fn from(s: &str) -> Person {
        let (name, age) = match s.split_once(',') {
            Some((name, age)) => (name.trim(), age.trim()),
            _ => return Person::default(),
        };

        if let Ok(age) = age.parse::<usize>() {
            if name.len() > 0 {
                return Person {
                    name: String::from(name),
                    age,
                };
            }
        }

        Person::default()
    }
}
```
---
### <font face="黑体" color=purple>from_str</font>
```rust


impl FromStr for Person {
    type Err = ParsePersonError;
    fn from_str(s: &str) -> Result<Person, Self::Err> {
        if s.is_empty() {
            return Err(ParsePersonError::Empty);
        }

        let splitted_item = s.split(',').collect::<Vec<&str>>();
        let (name, age) = match &splitted_item[..] {
            [name, age] => (
                name.to_string(),
                age.parse().map_err(ParsePersonError::ParseInt)?,
            ),
            _ => return Err(ParsePersonError::BadLen),
        };

        if name.is_empty() {
            return Err(ParsePersonError::NoName);
        }

        Ok(Person {
            name: name.into(),
            age,
        })
    }
}

```
### <font face="黑体" color=purple>try_from_into</font>
```rust
// Tuple implementation
impl TryFrom<(i16, i16, i16)> for Color {
    type Error = IntoColorError;
    fn try_from(tuple: (i16, i16, i16)) -> Result<Self, Self::Error> {
        let (red, green, blue) = tuple;

        for color in [red, green, blue] {
            if !(0..=255).contains(&color) {
                return Err(IntoColorError::IntConversion);
            }
        }
        Ok(Self {
            red: tuple.0 as u8,
            green: tuple.1 as u8,
            blue: tuple.2 as u8,
        })
    }
}

// Array implementation
impl TryFrom<[i16; 3]> for Color {
    type Error = IntoColorError;
    fn try_from(arr: [i16; 3]) -> Result<Self, Self::Error> {
        for color in arr {
            if !(0..=255).contains(&color) {
                return Err(IntoColorError::IntConversion);
            }
        }
        Ok(Self {
            red: arr[0] as u8,
            green: arr[1] as u8,
            blue: arr[2] as u8,
        })
    }
}

// Slice implementation
impl TryFrom<&[i16]> for Color {
    type Error = IntoColorError;
    fn try_from(slice: &[i16]) -> Result<Self, Self::Error> {
        if slice.len() != 3 {
            return Err(IntoColorError::BadLen);
        }
        for color in slice {
            if !(0..=255).contains(color) {
                return Err(IntoColorError::IntConversion);
            }
        }
        Ok(Self {
            red: slice[0] as u8,
            green: slice[1] as u8,
            blue: slice[2] as u8,
        })
    }
}
```

### <font face="黑体" color=purple>try_from_into</font>
```rust
// Tuple implementation
impl TryFrom<(i16, i16, i16)> for Color {
    type Error = IntoColorError;
    fn try_from(tuple: (i16, i16, i16)) -> Result<Self, Self::Error> {
        let (red, green, blue) = tuple;

        for color in [red, green, blue] {
            if !(0..=255).contains(&color) {
                return Err(IntoColorError::IntConversion);
            }
        }
        Ok(Self {
            red: tuple.0 as u8,
            green: tuple.1 as u8,
            blue: tuple.2 as u8,
        })
    }
}

// Array implementation
impl TryFrom<[i16; 3]> for Color {
    type Error = IntoColorError;
    fn try_from(arr: [i16; 3]) -> Result<Self, Self::Error> {
        for color in arr {
            if !(0..=255).contains(&color) {
                return Err(IntoColorError::IntConversion);
            }
        }
        Ok(Self {
            red: arr[0] as u8,
            green: arr[1] as u8,
            blue: arr[2] as u8,
        })
    }
}

// Slice implementation
impl TryFrom<&[i16]> for Color {
    type Error = IntoColorError;
    fn try_from(slice: &[i16]) -> Result<Self, Self::Error> {
        if slice.len() != 3 {
            return Err(IntoColorError::BadLen);
        }
        for color in slice {
            if !(0..=255).contains(color) {
                return Err(IntoColorError::IntConversion);
            }
        }
        Ok(Self {
            red: slice[0] as u8,
            green: slice[1] as u8,
            blue: slice[2] as u8,
        })
    }
}
```

### 最后一个

```rust
// Add the AsRef trait appropriately as a trait bound
fn byte_counter<T: AsRef<str>>(arg: T) -> usize {
    arg.as_ref().as_bytes().len()
}

// Obtain the number of characters (not bytes) in the given argument
// Add the AsRef trait appropriately as a trait bound
fn char_counter<T: AsRef<str>>(arg: T) -> usize {
    arg.as_ref().chars().count()
}

// Squares a number using AsMut. Add the trait bound as is appropriate and
// implement the function body.
fn num_sq<T: AsMut<u32>>(arg: &mut T) {
    *arg.as_mut() *= *arg.as_mut()
}
```






<span id = "末行锚点"></span>

---

<center><font face="华文行楷" style="font-size:20px"> 少年，我观你骨骼清奇，颖悟绝伦，必成人中龙凤。</font>
<center><font face="华文行楷" style="font-size:20px">不如点赞·收藏·关注一波</font>


<p align="center"><a  href="https://blog.csdn.net/qq_43840665/article/details/127674694"><img src="https://img-blog.csdnimg.cn/19de6fde1c994db39cc425ed0e87f492.gif"  width="500px" height="300px" ></a></p>

---

**🚩[点此跳转到首行↩︎](#首行锚点)**
## 参考博客
1. [ Rust语言圣经(Rust Course)]( https://course.rs/basic/ownership/borrowing.html  )
2. [ rust 的引用与借用 ]( https://zhuanlan.zhihu.com/p/306650851 )
3. [ Rust 学习笔记]( https://blog.csdn.net/qq_32303495/article/details/126870107 )
4. [ rustlilngs 答案]( https://github.com/aliyyousuff/rustlings-solutions )
5. [ Rust中some的用法](https://www.zhihu.com/question/389859557/answer/1174120773  )
6. [ 组合器](https://zhuanlan.zhihu.com/p/342525435 )
7. [ Rust：Trait]( https://zhuanlan.zhihu.com/p/127365605 )
8. [ Rust三种iterator(iter,iter_mut,into_iter)的区别 ](https://gongdear.com/articles/2020/12/28/1609152963317.html)
9. [Rust学习记录 -＞ 线程Thread](https://blog.csdn.net/weixin_45704680/article/details/121103371)
10. [RustCow](https://juejin.cn/post/7221969436885631033)
11. [Rust学习记录 -＞ 线程Thread](https://blog.csdn.net/weixin_45704680/article/details/121103371)
 

