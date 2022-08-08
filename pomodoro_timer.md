
## 第 001 个番茄时间

    时间：2022.01.05 01:02
    内容：Programming Rust 第160-164页。

## 第 002 个番茄时间

    时间：2022.01.05 23:20
    内容：Programming Rust 第164-167页。

## 第 003 个番茄时间

    时间：2022.01.06 00:47
    内容：Programming Rust 第167-172页。 Rust的Result错误处理方式真的很有好处吗？

## 第 004 个番茄时间

    时间：2022.01.06 23:53
    内容：Programming Rust 第173-176页。 

## 第 005 个番茄时间

    时间：2022.01.07 00:57
    内容：Programming Rust 第176-179页。 关于版本控制可进一步参考：The Edition Guide(https://doc.rust-lang.org/edition-guide/)。

## 第 006 个番茄时间

    时间：2022.01.08 13:30
    内容：Programming Rust 第179-184页。 主要是关于模块的内容(Modules)。
    
## 第 007 个番茄时间

    时间：2022.01.08 18:14
    内容：Programming Rust 第185-187页。 静态变量(Statics) and 常量（Constants）～～～ 常量在编译时编译器将直接用其值进行替代～～～    lazy_static是一个处理static的常用库

## 第 008 个番茄时间

    时间：2022.01.08 19:58
    内容：Programming Rust 第188-191页。 lib项目的src/bin目录中写可执行程序代码（通常比较合适高度依赖当前lib的轻量程序）。

## 第 009 个番茄时间

    时间：2022.01.09 01:14
    内容：Programming Rust 第192-196页。 主要关于rust的属性参数（如#[cfg(target_os="linux")]），test模块。。。

## 第 010 个番茄时间

    时间：2022.01.09 13:28
    内容：Programming Rust 第197-200页。 模块测试、继承测试、文档、文档测试～～～

## 第 011 个番茄时间

    时间：2022.01.09 14:54
    内容：Programming Rust 第201-202页。 通过在注释中的代码前面加上`#`，可以不影响文档测试，但在生成的文档中隐藏。  no_run 注释。ignore注释。 特殊依赖（git / path）

## 第 012 个番茄时间

    时间：2022.01.09 16:46
    内容：Programming Rust 第203-205页。 Cargo.toml中的[语义化版本](https://semver.org/lang/zh-CN/)； 发布crate。。。（cargo package; cargo login <apikey>; cargo publish）

## 第 013 个番茄时间

    时间：2022.01.09 17:40
    内容：Programming Rust 第206-208页。 工作空间(Workspaces，共享build目录和Cargo.lock)。 `cargo build --workspace` 编译工作空间中的所有crate。  Travis CI 值得了解和学习；cargo-readme值得使用～～～

## 第 014 个番茄时间

    时间：2022.01.09 18:39
    内容：Programming Rust 第209-211页。 具名结构体(Named-Field Structs)~~~

## 第 015 个番茄时间

    时间：2022.01.09 22:50
    内容：Programming Rust 第212-215页。 类元祖结构体(Tuple-Like Structs)~~~ 用.0 .1 .2 方式访问元素(elements)，相较于具名结构体，类元祖结构体更适合在模式匹配的情况下使用。。。   类单元结构体(Unit-Like Structs)~~~ 无元素的结构体（空结构），很像unit类型`()`。  结构体存储布局～～`#[repr(C)]`属性

## 第 016 个番茄时间

    时间：2022.01.10 01:25
    内容：Programming Rust 第215-217页。 给结构添加方法～～～  智能指针(Box, Rc, Arc)？   此处需要再细细琢磨～～～

## 第 017 个番茄时间

    时间：2022.01.10 18:20
    内容：Programming Rust 第217页。 通过Box指针将特殊的数据（如递归一样大小不确定的类型、大量数据所有权传递的、实现trait类型）包装到heap上？
    
    ```rust
        #[derive(Debug)]
        struct Node<T> {
            value: T,
            next: Box<Option<Node<T>>>
        }
        let list = Node {
            value: 1,
            next: Box::new(Some(Node {
                value: 1,
                next: Box::new(None)
            }))
        };
        println!("{:?}", list);
        // Node { value: 1, next: Some(Node { value: 1, next: None }) }
    ```

## 第 018 个番茄时间

    时间：2022.01.11 00:37
    内容： 
        智能指针 https://rustwiki.org/zh-CN/book/ch15-00-smart-pointers.html。
        智能指针区别于常规结构体的显著特性在于其实现了 Deref 和 Drop trait。
        常用智能指针：String 和 Vec<T>
        Deref trait 允许智能指针结构体实例表现的像引用一样，这样就可以编写既用于引用、又用于智能指针的代码。
        Drop trait 允许我们自定义当智能指针离开作用域时运行的代码。

        ```
        enum List {
            Cons(i32, List),
            Nil,
        }
        //  List 的一个成员被定义为是递归的：它直接存放了另一个相同类型的值。这意味着 Rust 无法计算为了存放 List 值到底需要多少空间。  故而编译失败。
        ```
        未完待续。。。  https://rustwiki.org/zh-CN/book/ch15-01-box.html#%E8%AE%A1%E7%AE%97%E9%9D%9E%E9%80%92%E5%BD%92%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%A4%A7%E5%B0%8F


## 第 019 个番茄时间

    时间：2022.01.11 23:02
    内容：  Rust 程序设计语言 中文版 15.1 
        使用 Box<T> 给递归类型一个已知的大小，打破编译过程中存储空间计算时的无限递归。
        ```
        enum List {
            Cons(i32, Box<List>),
            Nil,
        }
        ```
        通过 Deref trait 将智能指针当作常规引用处理（即解引用：*y ）。
        ```
            use std::ops::Deref;

            struct MyBox<T>(T);

            impl<T> Deref for MyBox<T> {
                type Target = T;        // 定义用于Deref trait 的关联类型。

                fn deref(&self) -> &T {
                    &self.0
                }
            }

            // *y 实际被解析为：*(y.deref())
        ```
        未完待续。。。。。   已实现Deref trait的类型之解引用强制转换（deref coercions）。

## 第 020 个番茄时间

    时间：2022.01.13 01:24
    内容：https://rustwiki.org/zh-CN/book/ch15-02-deref.html
        当所涉及到的类型定义了 Deref trait，Rust 会分析这些类型并可以任意多次调用 Deref::deref方法以获得匹配参数的类型。
        DerefMut trait 用于重载可变引用的 * 运算符。
        当 T: Deref<Target=U> 时从 &T 到 &U。
        当 T: DerefMut<Target=U> 时从 &mut T 到 &mut U。
        当 T: Deref<Target=U> 时从 &mut T 到 &U。
        ---------------
        Drop trait是智能指针第二个重要的trait，允许我们在值要离开作用域时执行一些代码（drop方法）。未完待续。。。

## 第 021 个番茄时间

    时间：2022.01.14 00:03
    内容：https://rustwiki.org/zh-CN/book/ch15-03-drop.html
        Drop trait的drop方法就是通常意义上的析构函数。
        Drop trait的drop方法是不能够被主动调用的（会造成double free的问题）。当我们希望在作用域结束之前就强制释放变量的话，我们应该使用的是由标准库提供的 std::mem::drop。
        -------------------
        Rc<T> 引用计数智能指针（Reference Counting）

## 第 022 个番茄时间

    时间：2022.01.14 17:21
    内容：https://rustwiki.org/zh-CN/book/ch15-04-rc.html
        每次调用Rc:clone(&T)，则Rc<T>中数据的引用计数会加1，而不是进行“深拷贝”。 也可以T.clone()。
        Rc::strong_count(&T) 可获取引用计数值。
        Rc<T>只允许多个不可变引用，因为：相同位置的多个可变借用可能造成数据竞争和不一致。
        通过内部可变性模式和 RefCell<T> 类型，可以与 Rc<T> 结合使用来处理不可变性的限制。

        待延展阅读：[Rust 中几个智能指针的异同与使用场景](https://ipotato.me/article/57)

## 第 023 个番茄时间

    时间：2022.01.14 19:50
    内容：https://rustwiki.org/zh-CN/book/ch15-05-interior-mutability.html
        内部可变性（Interior mutability）是 Rust 中的一个设计模式，它允许你即使在有不可变引用时也可以改变数据，这通常是借用规则所不允许的。
        RefCell<T> 用于能够确保代码遵守借用规则，但编译器不能理解和确定的情况，使代码在运行时检查借用规则，而非编译过程中检查借用规则。

        - Rc<T> 允许相同数据有多个所有者；Box<T> 和 RefCell<T> 有单一所有者。
        - Box<T> 允许在编译时执行不可变或可变借用检查；Rc<T>仅允许在编译时执行不可变借用检查；RefCell<T> 允许在运行时执行不可变或可变借用检查。
        - 因为 RefCell<T> 允许在运行时执行可变借用检查，所以我们可以在即便 RefCell<T> 自身是不可变的情况下修改其内部的值。

        内部可变性的用例：mock 对象

        待延展阅读：停机问题（Halting Problem）

## 第 024 个番茄时间

    时间：2022.01.15 01:00
    内容：https://rustwiki.org/zh-CN/book/ch15-05-interior-mutability.html
        内部可变性的用例：mock 对象
        PS：阅读用例代码，发现关于生命周期的知识又迷糊了。。。。。   FUCK。。。

## 第 025 个番茄时间

    时间：2022.01.15 22:11
    内容：RefCell<T> 在运行时记录借用。
        borrow方法 --> Ref<T>类型的智能指针 --> 不可变借用(可同时存在多个)
        borrow_mut方法 --> RefMut<T>类型的智能指针 --> 可变借用(只能存在一个)
        --------------------
        结合 Rc<T> 和 RefCell<T> 来拥有多个可变数据所有者。
        Cell<T> ？？？
        Mutex<T>提供线程间安全的内部可变性。

## 第 026 个番茄时间

    时间：2022.01.16 01:34
    内容：https://rustwiki.org/zh-CN/book/ch15-06-reference-cycles.html
        Rust 并不保证完全地避免内存泄漏。 Rc<T> 和 RefCell<T> 可以创建出循环引用，导致数据可以永远不被清除（内存泄漏）。创建引用循环是一个程序上的逻辑 bug。
        避免引用循环：将 Rc<T> 变为 Weak<T>。
        调用 Rc::downgrade 时会得到 Weak<T> 类型的智能指针。不同于将 Rc<T> 实例的 strong_count 加1，调用 Rc::downgrade 会将 weak_count 加1。使用 Weak<T> 所指向的值时，需要先尝试upgrade()方法，返回Some表示目标值还存在，否者返回None。

## 第 027 个番茄时间

    时间：2022.01.16 14:44
    内容：https://rustwiki.org/zh-CN/book/ch15-06-reference-cycles.html
        在树结构中，父节点拥有子节点，但子节点不应该拥有父节点(循环引用)，然而子节点可以知道其父节点(即弱引用)。

        Box<T> 有一个已知的大小并指向分配在堆上的数据。
        Rc<T> 记录了堆上数据的引用数量以便可以拥有多个所有者。
        RefCell<T> 和其内部可变性提供了一个可以用于当需要不可变类型但是需要改变其内部值能力的类型，并在运行时而不是编译时检查借用规则。

        返回《Programming Rust》217页   Passing Self as a Box, Rc, or Arc

## 第 028 个番茄时间

    时间：2022.01.16 15:38
    内容：Programming Rust 第217-219页。
        用impl为结构定义方法时，第一个参数可以是引用(&self, &mut self)或者自身(self，涉及到所有权转移)。将其他实例引用或拥有当前实例时，需要把Self封装到Box, Rc, Arc中。。。

## 第 029 个番茄时间

    时间：2022.01.16 16:20
    内容：Programming Rust 第219-220页。
        impl块定义函数时也可以不用self作为参数。
        参数含有self --> （实例的）方法？ --> T.some_method()
        参数不含self --> 类型关联函数？ (type-associated functions) --> T::some_function()
        --------------
        关联常量(Associated Consts)，即关联在特定类型上的常量。
        ```
        pub struct Vector2 { x: f32,
                            y: f32, 
                        }
        impl Vector2 {
            const ZERO: Vector2 = Vector2 { x: 0.0, y: 0.0 }; 
            const UNIT: Vector2 = Vector2 { x: 1.0, y: 0.0 };
        }
        ```

## 第 030 个番茄时间

    时间：2022.01.16 19:11
    内容：Programming Rust 第220-223页。
        关联常量的访问 -->  `::`，除了关联本身类型外，也可以关联别的类型。
        ---------
        泛型结构体(Generic Structs)
        ```
        pub struct Queue<T> { 
                older: Vec<T>,
                younger: Vec<T>
            }
        ```
        Queue<T>中的T读作：对于任意元素类型T，，，，  T叫做类型参数
        impl<T> Queue<T> 读作：对于任何类型T，以下部分定义Queue<T>实现的关联函数。 impl<T> 表明如下实现是正对任意类型T的。 在代码块中 Self 等同于 Queue<T>。 

## 第 031 个番茄时间

    时间：2022.01.17 08:00
    内容：Programming Rust 第223-225页。
        使用生命周期参数的结构体。（Structs with Lifetime Parameters）
        如果结构体中包含有引用，那么这些引用必须指定生命周期。在一个函数中，如果返回类型中使用的生命周期参数与输入参数的生命周期相同，则可以省略不写。
        ------------------
        Deriving Common Traits for Struct Types
        ```
        #[derive(Copy, Clone, Debug, PartialEq)]
        struct Point { 
            x: f64,
            y: f64
        }
        ```

## 第 032 个番茄时间

    时间：2022.01.17 21:27
    内容：Programming Rust 第225-228页。
        Interior Mutability 内部可变性
        Cell<T>, 针对存放在栈中的（实现了Copy trait的）值。
        RefCell<T>, 支持引用值。

        Cell<T>
        cell.get()
        cell.set()

        RefCell::new(value)
        ref_cell.borrow() --> Ref<T>, 共享引用。
        ref_cell.borrow_mut() --> RefMut<T>, 可变引用。
        ref_cell.try_borrow(), ref_cell.try_borrow_mut()，出错时返回Error，而非直接Panic。

        以上两者非线程安全，后续(19章)讨论：Mutex<T>


## 第 033 个番茄时间

    时间：2022.01.17 23:32
    内容：Programming Rust 第229-232页。
        Enums and Patterns (枚举和模式)
        枚举值转换成整数是允许的，反之则不行。但可以自行实现，
        枚举也可以和结构体一样实现(impl)方法。

## 第 034 个番茄时间

    时间：2022.01.19 00:20
    内容：Programming Rust 第232-236页。
        Enums with Data：
        枚举值可以是三种结构体（Unit-Like 类型，Tuple-Like, 具名结构体）。
        Enums in Memory：
        在内存中，带数据的枚举存储为带标签的小整数（不保证顺序），外加足够存储字段内容的空间。
        Rich Data Structures Using Enums：

        serde_json::Value 枚举的定义：https://docs.serde.rs/serde_json/enum.Value.html
        ```
        pub enum Value {
            Null,
            Bool(bool),
            Number(Number),
            String(String),
            Array(Vec<Value>),
            Object(Map<String, Value>),
        }
        ```

## 第 035 个番茄时间

    时间：2022.01.19 10:23
    内容：Programming Rust 第236-239页。
        最常见的Generic Enums（泛型枚举）：
        ```
        enum Option<T> { 
            None,
            Some(T), 
        }
        enum Result<T, E> {
            Ok(T),
            Err(E), 
        }
        ```
        枚举的值不能直接访问和获取。

## 第 036 个番茄时间

    时间：2022.01.19 23:07
    内容：Programming Rust 第239-241页。
        Patterns。
        待拓展阅读：《Rust Design Patterns》 https://fomalhauthmj.github.io/patterns/

## 第 037 个番茄时间

    时间：2022.01.20 10:16
    内容：Programming Rust 第242-244页。
        Literals, Variables, and Wildcards in Patterns。
        Tuple and Struct Patterns。 匹配过程中，可以用 .. 来省略不关心的字段。 .. 语法称为 rest 模式。
        ```
            Some(Account { name, language, .. }) =>
                language.show_custom_greeting(name),
        ```
        Array and Slice Patterns。
        
## 第 038 个番茄时间

    时间：2022.02.06 19:44
    内容：Programming Rust 第245-246页。
        Reference Patterns。
        引用(Ref)的模式匹配......

## 第 039 个番茄时间

    时间：2022.02.07 10:26
    内容：Programming Rust 第247-249页。
        Match Guards, 加入if条件。
        ```
        match point_to_hex(click) {
            None => Err("That's not a game space."),
            Some(hex) if hex == current_hex => Err("You are already there! You must click somewhere else"),
            Some(hex) => Ok(hex)
            }
        ```
        多值匹配：用 ｜ 分隔多个可能的匹配值。 该符号可以理解为按位OR，但更应该理解为正则表达式的｜。
        范围匹配：..= 。 

        @ 绑定: x @ pattern，可理解为 x if (x match pattern)。 

## 第 040 个番茄时间

    时间：2022.02.08 12:00
    内容：Programming Rust 第249-250页。
        不可辩驳模式（irrefutable patterns）：适用于let,for,函数参数，闭包参数。
        可辩驳模式(refutable patterns): 适用于match, if let, while let。


## 第 041 个番茄时间

    时间：2022.02.09 
    内容：Programming Rust 第251-254页。
        特性及泛型：Rust中多态性的实现方式。

## 第 042 个番茄时间

    时间：2022.02.11 00:35
    内容：Programming Rust 第254-256页。
        Trait为包括内建类型在内的各种类型添加拓展方法。
        Self类型，关联函数，关联类型，，，，

        特征(trait)代表一种能力：一个类型是否能做什么事儿～
        调用类型的trait方法时，相关trait必须要被导入(use <trait>)，以避免可能的重名冲突。
        trait方法类似于C++/C#中的虚拟方法。

        &mut dyn Write 如此类形式会产生动态调度开销。
        dyn Write 被称为“特征对象”(trait object)。
        ---------------
        在Rust中有两种通过trait实现多态的方式：特征对象(trait object)和泛型(generics)。

## 第 043 个番茄时间

    时间：2022.02.12 00:30
    内容：Programming Rust 第256-257页。
        特征对象（Trait Objects）: 一个指向trait类型的引用。
        Rust 不允许`dyn Write`类型的变量，因为实现Write特征的类型的具体大小是未知的，这违反了Rust需要知道类型大小的编译要求。
        Java中类似Write的接口OutputStream实际上是一个引用，因此，Rust中声明特征的变量时应该声明为引用。
        类似于： ` let writer: &mut dyn Write = &mut buf; `，此处的writer即是特征对象(trait object)。

        特征对象的不同之处在于，Rust在编译时通常不知道引用的具体类型。

        --------------------

        特征对象的布局：
        特征对象含有两个指针(占两个机器字节)，分别指向具体值和值类型。

        C++有类似的运行时类型，称为 virtual table (或vtable)。

## 第 044 个番茄时间

    时间：2022.02.12 16:13
    内容：Programming Rust 第258-259页。
        Box<dyn Write>和&mut dyn Write一样，是一个胖指针：它包含值本身的地址和vtable的地址。其他指针类型也是如此，如Rc<dyn Write>。
        ------------
        泛型函数及类型参数（Generic Functions and Type Parameters）：
        以特征对象作为参数的函数可以转化为泛型函数：
        ```
        fn say_hello(out: &mut dyn Write) // plain function 
        fn say_hello<W: Write>(out: &mut W) // generic function, <W: Write>即是类型参数。
        ```
        调用时：
        ```
        say_hello(&mut local_file)?; // calls say_hello::<File>
        say_hello::<File>(&mut local_file)?;  // 可以指明参数类型，但非必要(rust可以自动推测)
        ```
        某些情况必须要声明参数类型(type parameters):
        ```
        // calling a generic method collect<C>() that takes no arguments 
        let v1 = (0 .. 1000).collect(); // error: can't infer type
        let v2 = (0 .. 1000).collect::<Vec<i32>>(); // ok
        ```

## 第 045 个番茄时间

    时间：2022.02.12 23:55
    内容：Programming Rust 第259-261页。
        类型参数可同时声明多个trait。如：
        ```
        fn top_ten<T: Debug + Hash + Eq>(values: &Vec<T>) { ... }
        -------
        fn run_query<M: Mapper + Serialize, R: Reducer + Serialize>(data: &DataSet, map: M, reduce: R) -> Results
        {...}
        ```
        泛型函数可以有多个类型参数，为了便于书写阅读，可以将类型参数声明在where分句：
        ```
        fn run_query<M, R>(data: &DataSet, map: M, reduce: R) -> Results
            where   M: Mapper + Serialize,
                    R: Reducer + Serialize
            {...}
        ```
        这样的where分句同样可以用在泛型结构体、枚举、类型别称、方法等任何允许bounds的地方。

        泛型函数可以同时具有生命周期参数和类型参数。

## 第 046 个番茄时间

    时间：2022.02.13 01:06
    内容：Programming Rust 第261-262页。
        特征对象与泛型的使用区别～～～
        通过特征对象实现的代码相比于泛型的，少了一些代码肿胀(code bloat)？
        一般地，泛型更具有优势：1, 不使用dyn关键词(没有涉及特征对象）因此不涉及动态调度，故而运行速度更快。2, 并非所有的trait都支持trait object；例如关联函数只能使用泛型。3, 泛型可以多个trait约束到类型参数，而trait object不能实现。

## 第 047 个番茄时间

    时间：2022.02.13 12:11
    内容：Programming Rust 第262-264页。
        特征对象在编译时不知道具体对象类型，只有在运行时才知道。
        --------------------
        [Defining and Implementing Traits]

## 第 048 个番茄时间

    时间：2022.02.13 15:44
    内容：Programming Rust 第264-267页。
        为类型实现trait方法：
        ```
        impl Visible for Broom {...}
        ```
        为类型实现独立的方法：
        ```
        impl Broom {
                fn fun01() ....
        }
        ```
        [Default Methods]
        Iterator trait除了一个需要实现的方法(.next())外，拥有数十个默认方法。

        [Traits and Other People’s Types]
        可以使用泛型impl块一次性向整个类型系列添加扩展特征(extension trait)。
        ```
        /// You can write HTML to any std::io writer.
        /// 为所有实现了Write trait的泛型W实现WriteHtml方法。
        impl<W: Write> WriteHtml for W {
            fn write_html(&mut self, html: &HtmlDocument) -> io::Result<()> {
            ... }
        }
        ```
        

## 第 049 个番茄时间

    时间：2022.02.13 17:55
    内容：Programming Rust 第267-269页。
        Rust孤儿规则(orphan rule)：
            1. 当你为某类型实现某 trait 的时候，必须要求类型或者 trait 至少有一个是在当前 crate 中定义的。你不能为第三方的类型实现第三方的 trait 。
            2. 在调用 trait 中定义的方法的时候，一定要记得让这个 trait 可被访问。
        
        [Self in Traits]
        trait可以把关键字Self作为类型。
        使用Self类型的trait与 trait object是不兼容的：
        ```
        // error: the trait `Spliceable` cannot be made into an object
        fn splice_anything(left: &dyn Spliceable, right: &dyn Spliceable) { 
            let combo = left.splice(right);
            // ...
        }
        ```
        Rust拒绝此代码，因为left.splice(right)无法通过编译器的类型检查，left和right都需要在运行时确定值类型，可能出现类型不匹配。

## 第 050 个番茄时间

    时间：2022.02.13 21:05
    内容：Programming Rust 第269-271页。
        [Subtraits]
        trait object不能支持同时声明多个trait，但可以通过subtrait来处理：将trait的拓展(extension)定义为新拓展。
        ```
        trait Creature: Visible { }
        // Creature是Visible的子特征(subtrait)，Visible是Creature的超级特征(supertrait)。
        -----------------
        trait Creature where Self: Visible { }  // 本质写法
        ```
        subtrait类似于C#中的子接口，但在Rust中，subtrait不会继承supertrait的关联项。

        [Type-Associated Functions] 类型关联函数？ 类似于面向对象中的静态方法～
        ```
        trait StringSet {
            fn new() -> Self;    // 参数中不含&self，即为type-associated function??? 通过StringSet::new()调用？（此处可能理解有误）
            fn contains(&self, string: &str) -> bool;
        ```
        与Java和C#接口一样，trait object不支持type-associated function？？？

## 第 051 个番茄时间

    时间：2022.02.13 23:37
    内容：《Programming Rust 2nd Edition》第271-273页。
        [Fully Qualified Method Calls]完全限定名调用
        ```
        "hello".to_string()
        str::to_string("hello")
        ToString::to_string("hello")   // to_string是ToString trait的一种方法。
        <str as ToString>::to_string("hello")   // a fully qualified method call
        ```
        使用完全限定名调用的原因：
        1. 方法重名。
        2. self参数的类型不能推测。
        3. 函数本身作为函数值时。 ？？？ 不理解
        4. 在宏中调用trait方法时。

## 第 052 个番茄时间

    时间：2022.02.14 10:28
    内容：《Programming Rust 2nd Edition》第273-275页。
        [Traits That Define Relationships Between Types] 定义类型间关系的trait
        [Associated Types (or How Iterators Work)]关联类型
        ```
        pub trait Iterator {
            type Item;   // associated type, 关联类型； 
            // 实现Iterator的每个类型都必须指定它生成的item类型。
            fn next(&mut self) -> Option<Self::Item>;
            ...
        }
        ```
        Item(即：<I as Iterator>::Item)是每种迭代器类型的feature，而不是独立的类型。
        ```
        // (code from the std::env standard library module)
        impl Iterator for Args {
            type Item = String;
            fn next(&mut self) -> Option<String> {
                ...
            }
            ... 
        }
        ```

## 第 053 个番茄时间

    时间：2022.02.14 14:43
    内容：《Programming Rust 2nd Edition》第275-277页。
        除了associated Item type，还有associated Output type，associated Match type。

        关联类型非常适合于每一个实现都有一个特定相关类型的情况：每种Task类型都产生特定的Output类型；每种Pattern类型都查找特定的Match类型。？？？

## 第 054 个番茄时间

    时间：2022.02.14 23:09
    内容：《Programming Rust 2nd Edition》第277-278页。
        [Generic Traits (or How Operator Overloading Works)] 泛型特征
        min::<i32> 与 min::<String> 是不同的函数。min::<T>
        Vec<i32> 与 Vec<String> 是不同的类型。  Vec<T>
        Mul<f64> 与 Mul<String> 是不同的trait。 Mul<RHS>

        orphan rule孤儿规则的例外：当trait的类型参数定义在当前crate时，可以为外部类实现外部trait。

        在Rust中，lhs * rhs 是Mul::mul(lhs, rhs)的缩写。因此，在Rust中重载*运算符就像实现Mul trait一样简单。

## 第 055 个番茄时间

    时间：2022.02.15 00:33
    内容：《Programming Rust 2nd Edition》第278-280页。
        [impl Trait]    ？？？？  这部分真够难懂的～～～～
        impl Trait允许我们“抹去”返回值的类型，仅返回某个trait。 即简化代码也便于统一类型签名。
        ```
        fn cyclical_zip(v: Vec<u8>, u: Vec<u8>) -> iter::Cycle<iter::Chain<IntoIter<u8>, IntoIter<u8>>> {
            v.into_iter().chain(u.into_iter()).cycle()
        }
        -------------------
        fn cyclical_zip(v: Vec<u8>, u: Vec<u8>) -> Box<dyn Iterator<Item=u8>> { 
            Box::new(v.into_iter().chain(u.into_iter()).cycle())
        }
        -------------------
        fn cyclical_zip(v: Vec<u8>, u: Vec<u8>) -> impl Iterator<Item=u8> {
            v.into_iter().chain(u.into_iter()).cycle()
        }
        ```
        impl Trait 是一种静态分发形式（故而不能由动态值控制）。
        需要注意的是，rust不允许trait的方法将impl Trait作为返回值。
        
## 第 056 个番茄时间

    时间：2022.02.15 11:03
    内容：RFC: impl trait
        [RFC导读：impl trait](https://zhuanlan.zhihu.com/p/26516100)
            impl Trait 这个语法，在某些场景下，具有明显优势，可以提高语言的表达能力。但是，要把它推广到各个场景下使用，还需要大量的设计和实现工作。目前的这个RFC将目标缩小为了：先推进这个语法在函数参数和返回值场景下使用，其它的情况，后面再考虑。
            不要过于激进地使用这个功能，在每个可以使用 impl Trait 的地方都用它替换原先的具体类型。它更多的倾向于简洁性，而牺牲了一部分表达能力。
            

            [Stabilize impl Trait](https://github.com/rust-lang/rust/pull/49255)
            [Tracking issue for impl Trait (RFC 1522, RFC 1951, RFC 2071)](https://github.com/rust-lang/rust/issues/34511)

            1.26版本引入的存在类型(existential type)，通过impl trait实现。

        // -----------------------------
        rust中返回trait对象的方法:
            方法一：引入Box （trait object)，Box<dyn TraitName>
            方法二：impl trait
        
        // -----------------------------
        impl dyn Trait？？？？

## 第 057 个番茄时间

    时间：2022.02.15 21:41
    内容：《Programming Rust 2nd Edition》第280-284页。
        [Associated Consts]关联常数
        类似于关联类型和关联函数，关联常数可以不预先赋值，而在实现中进行赋值。

        [Reverse-Engineering Bounds]逆向工程约束？？？

        [Traits as a Foundation]

## 第 058 个番茄时间

    时间：2022.02.15 23:11
    内容：《Programming Rust 2nd Edition》第285-288页。
        [CHAPTER 12 - Operator Overloading]
            [Arithmetic and Bitwise Operators]

## 第 059 个番茄时间

    时间：2022.02.16 01:06
    内容：《Programming Rust 2nd Edition》第289-290页。
        [Unary Operators] 一元运算符
        运算符'!'同时具有bool型取反和按位取反的能力。
        ```
        use std::ops::Neg;
        impl<T> Neg for Complex<T>
        where
            T: Neg<Output = T>, 
        {
            type Output = Complex<T>;
            fn neg(self) -> Complex<T> {
                    Complex {
                        re: -self.re,
                        im: -self.im,
                    }
            }
        }
        ```
        [Binary Operators] 二元运算符
        ```
        trait BitXor<Rhs = Self> {
            type Output;
            fn bitxor(self, rhs: Rhs) -> Self::Output;
        }
        ```

## 第 060 个番茄时间

    时间：2022.02.16 11:11
    内容：关联类型（associated types）

        关联类型（associated types）是一个将类型占位符与 trait 相关联的方式，这样 trait 的方法签名中就可以使用这些占位符类型。trait 的实现者会针对特定的实现在这个类型的位置指定相应的具体类型。如此可以定义一个使用多种类型的 trait，直到实现此 trait 时都无需知道这些类型具体是什么。
        ```
        pub trait Watch {
            type Item;      // 关联类型
            fn inner(&self) -> Option<Self::Item>;
        }

        struct A {
            data: i32,
        }

        impl Watch for A {
            type Item = i32;
            fn inner(&self) -> Option<Self::Item> {
                Some(self.data)
            }
        }
        ```
        ---------------------
        Add<RHS = Self>是默认泛型类型参数，表示如果不显示指定泛型类型，就默认泛型类型为Self。
        ```
        pub trait Watch<Inner=String> {
            type Item;
            fn inner(&self) -> Option<Self::Item>;
            fn info(&self) -> Inner;
        }
        ------------------
        pub trait Add<RHS = Self> {
            type Output;

            #[must_use]
            fn add(self, rhs: RHS) -> Self::Output;
        }
        ```

        -------------------
        泛型关联类型(GAT)           https://zhuanlan.zhihu.com/p/369302538
        关联条目一共有三种：关联常数，关联函数，关联类型(别名)；它们与条目中的三种：常数、函数、类型(别名) 一一对应。

        任务#1：用泛型关联类型支持类型家族

        任务#2：用泛型关联类型实现流式处理迭代器


## 第 061 个番茄时间

    时间：2022.02.16 21:22
    内容：RFC - https://rust-lang.github.io/rfcs/1598-generic_associated_types.html
        Feature Name: generic_associated_types
        Start Date: 2016-04-29
        RFC PR: rust-lang/rfcs#1598
        Rust Issue: rust-lang/rust#44265

        Kinds：种类？ Kinds are often called 'the type of a type'
        Higher-kinded types：高级类型

        If you have a type like Foo<'a>, the kind of Foo is lifetime -> type
        vec::Iter<'a, T> vec::Iter 的种类(kind)是： lifetime, type -> type

        难懂的要死！！！

        [Features of associated type constructors]

## 第 062 个番茄时间

    时间：2022.02.16 23:12
    内容：RFC - https://rust-lang.github.io/rfcs/1598-generic_associated_types.html
        [Features of associated type constructors]

        WQNMLGB，太南了，宛如天书。

## 第 063 个番茄时间

    时间：2022.02.17 01:24
    内容：《Programming Rust 2nd Edition》第291-293页。
        [Compound Assignment Operators]
        复合赋值操作符与相同功能的二元操作符是完全独立的。 + 是实现的 std::ops::Add, += 是实现的std::ops::AddAssign。

        [Equivalence Comparisons] 等值比较
        ```
        trait PartialEq<Rhs = Self>
        where
                Rhs: ?Sized,     // 因为只是借用，不会转移所有权。
        {
            fn eq(&self, other: &Rhs) -> bool;
            fn ne(&self, other: &Rhs) -> bool {
                    !self.eq(other)
                }
        }

        impl<T: PartialEq> PartialEq for Complex<T> {
            fn eq(&self, other: &Complex<T>) -> bool {
                    self.re == other.re && self.im == other.im
                }
        }
        -------------
        // 可以直接在类型定义的derive属性中添加PartialEq，rust既可自动实现。
        #[derive(Clone, Copy, Debug, PartialEq)]
        struct Complex<T> {
            ...
        }
        ```

## 第 064 个番茄时间

    时间：2022.02.17 10:31
    内容：《Programming Rust 2nd Edition》第293-295页。
        `where Rhs: ?Sized,`约束用以满足rust要求类型参数大小可知。 后续会进一步探讨 sized type, unsized type, Sized trait。

        rust中，NaN != NaN 。 所以 PartialEq(partial equivalence relation，== )才作为rust的内建trait。

        rust的标准库中，只有f32,f64没有实现Eq，只实现了PartialEq。
        
        ```
        trait Eq: PartialEq<Self> {}

        impl<T: Eq> Eq for Complex<T> {}

        // --------------------------------
        // 只需在复杂类型定义的派生属性中包含Eq，即可完成实现。
        #[derive(Clone, Copy, Debug, Eq, PartialEq)]
            struct Complex<T> { ...
            }
        ```

## 第 065 个番茄时间

    时间：2022.02.18 00:18
    内容：《Programming Rust 2nd Edition》第295-297页。
        [Ordered Comparisons]
        ```
        trait PartialOrd<Rhs = Self>: PartialEq<Rhs>
        where
            Rhs: ?Sized,
        {
            fn partial_cmp(&self, other: &Rhs) -> Option<Ordering>;  // 唯一待实现的方法。

            fn lt(&self, other: &Rhs) -> bool { ... } 
            fn le(&self, other: &Rhs) -> bool { ... } 
            fn gt(&self, other: &Rhs) -> bool { ... } 
            fn ge(&self, other: &Rhs) -> bool { ... }
        }
        ```
        
## 第 066 个番茄时间

    时间：2022.02.18 01:39
    内容：《Programming Rust 2nd Edition》第298-300页。
        [Index and IndexMut]  索引

        [Other Operators] 其他运算符重载
        有些操作符不可重载：
            ?           错误检查操作符
            && / ||     逻辑运算符
            .. / ..=    ？？？
            &           引用操作符
            =           赋值操作符

        -------------------
        解引用操作符： * 

## 第 067 个番茄时间

    时间：2022.02.18 10:37
    内容：《Programming Rust 2nd Edition》第301-305页。
        [Utility Traits] 实用特征
        rust的utility traits主要有三类：
            1. 语言扩展traits。 Drop, Deref, DerefMut, From, Into
            2. 标记traits。 Sized, Copy
            3. 公共词汇traits。 Default, AsRef, AsMut, Borrow, BorrowMut, TryFrom, TryInto, ToOwned, Clone
        [Drop]
            Drop trait的drop()方法不可以被主动调用。
            一般只有在自定义类型中，需要释放rust不可知的资源时才实现Drop。

            如果类型实现Drop，则无法实现Copy。如果类型是Copy，这意味着简单逐字节复制足以生成该值的独立副本。

## 第 068 个番茄时间

    时间：2022.02.18 15:39
    内容：《Programming Rust 2nd Edition》第305-306页。
        [Utility Traits] - Sized
        其值在内存中大小相同的类型 -- sized type。 固定大小的类型
        Vec<T>是一个指针，所以也是sized type。
        
        所有的sized类型都实现了std::marker::Sized trait。

        Siezed只作为类似于 T:Sized 样式来约束某类型的变量，用以约束T在编译阶段大小可知。

        大小非总是相同的类型 -- unsized type。   非固定大小的类型

        string切片类型：str -- unsized type；但&str是 sized type。

        Array切片类型：[T] -- unsized type；但&[T]是 sized type。

        另一个众所周知的unsized类型：dyn 类型 -- 特征对象的参照？？？

        特征对象是指向实现给定特征的某些值的指针。（a trait object is a pointer to some value that implements a given trait.）

## 第 069 个番茄时间

    时间：2022.02.18 22:31
    内容：《Programming Rust 2nd Edition》第306-308页。
         T: ?Sized 表示：T不需要大小固定。
         如果声明 struct S<T: ?Sized> { b: Box<T> }，那么S<str>和S<dyn Write>是允许的。

        非固定大小类型(unsized type)不能存储自在变量中，也不能作为参数传递。。。。
        然而非固定大小类型也有优点：变量/参数可接受slices、trait objects类型的值。
        ?Sized约束 表示类型变量可以是Sized,也可以是Unsized。

        除了slices和trait objects外，结构体类型的最后一个字段可能是Unsized类型。
        ```
        struct RcBox<T: ?Sized>
        {
            ref_count: usize,
            value: T,
        }
        ```

## 第 070 个番茄时间

    时间：2022.02.19 13:28
    内容：《Programming Rust 2nd Edition》第308-310页。
        [Utility Traits] - Clone
        
        std::fs::File提供了try_clone方法。

        [Utility Traits] - Copy

        实现了Drop的类型不可以实现Copy，因为rust设定：如果一个类型剧要特殊的清理代码，那也需要特殊的复制代码。

        ---------------
        Copy 和 Clone 两者的区别和联系有：

        1. Copy内部没有方法，Clone内部有两个方法。
        
        2. Copy trait 是给编译器用的，告诉编译器这个类型默认采用 copy 语义，而不是 move 语义。Clone trait 是给程序员用的，我们必须手动调用clone方法，它才能发挥作用。
        
        3. Copy trait不是你想实现就实现，它对类型是有要求的，有些类型就不可能 impl Copy。Clone trait 没有什么前提条件，任何类型都可以实现（unsized 类型除外）。
        
        4. Copy trait规定了这个类型在执行变量绑定、函数参数传递、函数返回等场景下的操作方式。即这个类型在这种场景下，必然执行的是“简单内存拷贝”操作，这是由编译器保证的，程序员无法控制。Clone trait 里面的 clone 方法究竟会执行什么操作，则是取决于程序员自己写的逻辑。一般情况下，clone 方法应该执行一个“深拷贝”操作，但这不是强制的，如果你愿意，也可以在里面启动一个人工智能程序，都是有可能的。
        
        5. 如果你确实需要Clone trait执行“深拷贝”操作，编译器帮我们提供了一个工具，我们可以在一个类型上添加#[derive(Clone)]，来让编译器帮我们自动生成那些重复的代码。
        
        6. 然而Rust语言规定了当T: Copy的情况下，Clone trait代表的含义。即：当某变量let t: T;，符合T: Copy时， 它调用 let x = t.clone() 方法的时候，它的含义必须等同于“简单内存拷贝”。也就是说，clone的行为必须等同于let x = std::ptr::read(&t);，也等同于let x = t;。当T: Copy时，我们不要在Clone trait里面乱写自己的逻辑。所以，当我们需要指定一个类型是 Copy 的时候，最好顺便也指定它 Clone 的行为，就是编译器为我们自动生成的那个逻辑。正因为如此，在希望让一个类型具有 Copy 性质的时候，一般使用 #[derive(Copy, Clone)] 这种方式，这种情况下它们俩最好一起出现，避免手工实现 Clone 导致错误。

## 第 071 个番茄时间

    时间：2022.02.19 16:49
    内容：《Programming Rust 2nd Edition》第310-313页。
        [Utility Traits] - Deref and DerefMut
        可以通过实现std::ops::Deref和std::ops::DerefMut特征来指定 * 和 . 等解引用运算符在类型上的操作。

        ```
        trait Deref {
            type Target: ?Sized;
            fn deref(&self) -> &Self::Target;
        }
        trait DerefMut: Deref {
            fn deref_mut(&mut self) -> &mut Self::Target;
        }
        ```

        某类型实现了Deref<Target=T>，那么该类型可被解引用强制转换(deref coercions)为T类型。 比如String实现了Deref<Target=str>，所以可以在String上直接使用 str实现的方法，&String可以解引用强制转换为&str。

        Deref 和 DerefMut 特征不能用于类型变量的合法检测？？？？ 但可以通过 as 操作符先进行类型转换。

## 第 072 个番茄时间

    时间：2022.02.20 00:15
    内容：《Programming Rust 2nd Edition》第313-315页。
        [Utility Traits] - Default
        如果结构体的各字段都实现了Default，则可以使用#[derive(Default)]自动实现结构的默认值。

        [Utility Traits] - AsRef and AsMut
        如果一个类型实现了AsRef<T>，则可以有效地借用一个&T。AsMut -----> &mut T

        AsRef通常用于使函数在接受参数的类型中更加灵活。如此，任何实现了AsRef<T>的类型都可以被接受。

## 第 073 个番茄时间

    时间：2022.02.20 13:27
    内容：《Programming Rust 2nd Edition》第315-316页。
        字符串的字面量是&str，但实现AsRef<Path>的是str。 因为Rust不会尝试解引用强制转换类型去满足类型变量绑定，所以这里不会发生强制转型。。。。
        然而标准库包含有一个非限制性(blanket)的实现：  
        ```
        trait AsRef<T: ?Sized> {
            fn as_ref(&self) -> &T;
        }
        // ------------------------
        impl<'a, T, U> AsRef<U> for &'a T
            where   T: AsRef<U>,
                    T: ?Sized, U: ?Sized
        {
            fn as_ref(&self) -> &U {
                    (*self).as_ref()
                }
        }
        ```
        原理上大概可以猜测，但不能很好的理解代码～ ？？？？？？

        对于任意类型T和U，如果T:AsRef<U>，则&T:AsRef<U>也成立，即引用跟随。 str:AsRef<Path> 故而 &str:AsRef<Path>。  可以理解为有限制的解引用强制转型。

        同样，对于大部分情况，AsRef<T> ------> AsMut<T>。 不适用的情况是：如果修改T会影响对应类型的不变性约束，则不可以。 比如UTF8的字符串就不能够AsMut<T>。

## 第 074 个番茄时间

    时间：2022.02.20 16:20
    内容：《Programming Rust 2nd Edition》第316-319页。
        [Utility Traits] - Borrow and BorrowMut
        Borrow与AsRef存在什么区别？？？？？
        Borrow有更加严格的限制：只有当&T与它所借用的值具有相同hashes和比较特性时，该类型才能实现Borrow<T>。 （非Rust强制要求，但这是文档中规定的Borrow trait的意图）。这使得Borrow在处理哈希表或树中的键（或其他被hash或比较的值）时很有用。
        
        只有当&T散列和计算解析与借款价值相同时，类型才应实现Borrow<T>。

        [Utility Traits] - From and Into
        AsRef和AsMut是转换数据的借用类型。
        From和Into是直接转换数据本身的类型，也涉及到所有权转移。

        标准库中，对每种类型T都实现了From<T>和Into<T>。 通常Into比From更灵活。。。。

## 第 075 个番茄时间

    时间：2022.02.20 17:26
    内容：《Programming Rust 2nd Edition》第320-321页。
        From和Into转化可能比AsRef和AsMut需要更多的开销。
        ？运算符使用From和Into来帮助清理可能以多种方式失败的函数中的代码，方法是在需要时自动从特定的错误类型转换为常规错误类型。

        From和Into是绝对可靠的trait。  wrapping转换？  saturating(饱和)转换？

        [Utility Traits] - From and Into
        对于不确定如何转化为妥的情形，Rust中实现复杂一些的TryFrom和TryInto来替代From和Into。 对应的方法是：try_from() 和 try_into()。

## 第 076 个番茄时间

    时间：2022.02.20 18:05
    内容：《Programming Rust 2nd Edition》第322-323页。
        ```
        use std::convert::TryInto;
        // Saturate on overflow, rather than wrapping   饱和转换
        let smaller: i32 = huge.try_into().unwrap_or(i32::MAX);
        ```

        [Utility Traits] - ToOwned   ？？？？？？
        某些类型不能使用std::clone::Clone，如&str和&[i32]不能Clone。
        根据定义，克隆 &T 必须返回 T类型的值，而str 和 [u8] 都是unsized type, 它们甚至不能作为函数的返回类型。

        std::borrow::ToOwned trait提供了一个稍微宽松的方案来将引用转换成具有所有权的类型。
        ```
        trait ToOwned {
            type Owned: Borrow<Self>;
            fn to_owned(&self) -> Self::Owned;
        }
        ```
        Owned类型必须实现Borrow<Self>。 

        ？？？？

## 第 077 个番茄时间

    时间：2022.02.20 21:40
    内容：《Programming Rust 2nd Edition》第323-324页。
        [Utility Traits] - Borrow and ToOwned at Work: The Humble Cow     写时复制 / 写时克隆 -- 避免不必要的复制。
        函数参数接收值还是引用？ 这是一个问题～～～～，可用Cow类型来解决～  Clone-on-write，即写时克隆。本质上是一个智能指针。

        https://wiki.jikexueyuan.com/project/rust-primer/intoborrow/cow.html

        写时复制（Copy on Write）技术是一种程序中的优化策略，多应用于读多写少的场景。主要思想是创建对象的时候不立即进行复制，而是先引用（借用）原有对象进行大量的读操作，只有进行到少量的写操作的时候，才进行复制操作，将原有对象复制后再写入。这样的好处是在读多写少的场景下，减少了复制操作，提高了性能。

        -------------------------
        Rust的诸多trait仍旧不懂～～～～～

## 第 078 个番茄时间

    时间：2022.02.21 10:03
    内容：《Programming Rust 2nd Edition》第325-327页。
        [CHAPTER 14 -- Closures]
        [Closures - Capturing Variables]
        变量捕获～～～

## 第 079 个番茄时间

    时间：2022.02.21 19:35
    内容：《Programming Rust 2nd Edition》第328-330页。
        ```
        fn start_sorting_thread(mut cities: Vec<City>, stat: Statistic) -> thread::JoinHandle<Vec<City>>
        {
            let key_fn = move |city: &City| -> i64 { -city.get_statistic(stat) };   // 闭包key_fn获得了stat的所有权，如果stat是可复制值（如i32），那么此处执行的是复制操作。

            thread::spawn(move || { cities.sort_by_key(key_fn); cities})    // 此处闭包获得了cities和key_fn的所有权，因为Vec<City>是不可复制类型，所以此处cities转移到了新线程。
        }
        ```

        [Closures - Capturing Variables]
        [Function and Closure Types] 函数和闭包类型
        函数和闭包被当作值来使用，那他们理当有自己所属的类型。

        可以像使用其他类型一样来使用函数类型。

## 第 080 个番茄时间

    时间：2022.02.21 20:50
    内容：《Programming Rust 2nd Edition》第330-333页。
        一个函数可以接收另一个函数作为参数。

        效果相同（trait相同）的函数和闭包的类型是不同的。 如下泛型函数可实现同时接受闭包和函数。
        ```
        fn count_selected_cities<F>(cities: &Vec<City>, test_fn: F) -> usize
        where F: Fn(&City) -> bool
        {
            let mut count = 0; for city in cities {
                if test_fn(city) {
                    count += 1;
                }
            }
            count
        }
        ```

        `fn(&City) -> bool` // fn type (functions only)
        `Fn(&City) -> bool` // Fn trait (both functions and closures)

        函数的类型是fn, 而闭包有自己独特的类型（因为闭包可能包含从作用域中借来活偷来的数据），但是所有的闭包都实现了一个Fn trait。 比如： `Fn(&City) -> bool`。

        [Closure Performance]   闭包的性能

## 第 081 个番茄时间

    时间：2022.02.22 00:24
    内容：《Programming Rust 2nd Edition》第333-336页。
        [Closures and Safety]
        
        [FnOnce] FnOnce闭包只能被调用一次？
        调用Fn闭包时，实际调用closure.call(), 使用&self。
        调用FnOnce闭包时，实际调用closure.call_once()，使用self本身，将会被消费。

## 第 082 个番茄时间

    时间：2022.02.22 11:01
    内容：《Programming Rust 2nd Edition》第336-338页。
        [FnMut]
        从多个线程调用闭包读写同一数据时可能导致条件竞争～
        FnMut闭包可以用于写数据。 通过mut引用来调用～

        任何需要以mut方式访问值但不清除值的闭包都(应当)是mut闭包。

        - Fn闭包：可以多次调用。
        - FnMut闭包：self声明为mut，可以多次调用。
        - FnOnce闭包：调用者拥有该闭包，只能调用一次。

        Fn()是FnMut()的子trait，FnMut()是FnOnce()的子trait。

## 第 083 个番茄时间

    时间：2022.02.22 21:34
    内容：《Programming Rust 2nd Edition》第338-341页。
        [Copy and Clone for Closures]
        对于只包含共享引用变量的non-move闭包，变量实现了Clone和Copy，那么闭包也就实现了Clone和Copy。
        对于变量可变的non-move闭包，由于可变引用没有实现Clone和Copy，所以闭包也不能实现Clone和Copy。
        对于move闭包，如果闭包捕获的变量可Copy，那么闭包就可以Copy，Clone雷同。

        [Callbacks] 回调
        web服务端实现中，URL绑定的函数就是回调函数。

## 第 084 个番茄时间

    时间：2022.02.23 00:55
    内容：《Programming Rust 2nd Edition》第341-344页。
        每个闭包都具有不同的类型，因为每个闭包捕获不同的变量，因此它们也都具有不同的大小。

        [Using Closures Effectively]
        ????

## 第 085 个番茄时间

    时间：2022.02.23 10:58
    内容：《Programming Rust 2nd Edition》第345-346页。
        [CHAPTER 14 -- Iterators] 迭代器，闭包YYDS。
        表达式 1..=n 是 RangeInclusive<i32>值。
        ```
        fn triangle(n: i32) -> i32 {
            (1..=n).fold(0, |sum, item| sum + item)
        }
        ```
        fold(折叠)是高阶函数，其它的常见高阶函数还有：归约（reduce）、积累（accumulate）、聚集（aggregate）、压缩（compress）或注入（inject）。

## 第 086 个番茄时间

    时间：2022.02.23 22:01
    内容：《Programming Rust 2nd Edition》第347-348页。
        [The Iterator and IntoIterator Traits]
        如果某个类型想要实现迭代器，那么就需要为该类型实现std::iter::IntoIterator。即：实现了IntoIterator的类型就是可迭代类型。
        ```
        trait IntoIterator where Self::IntoIter: Iterator<Item=Self::Item> {
            type Item;
            type IntoIter: Iterator;
            fn into_iter(self) -> Self::IntoIter;
        }
        // IntoIter是迭代器值本身的类型，Item是它产生的值类型。
        ```
        vector的遍历，本质过程：
        ```
        // for element in &v {println!("{}", element);}

        let mut iterator = (&v).into_iter();
        while let Some(element) = iterator.next() {
                println!("{}", element);
            }

        // For loop使用IntoIterator::into_iter将其操作数&v转换为迭代器，然后反复调用Iterator::next。
        ```

        - 一个迭代器(iterator)是实现Iterator的任何类型。
        - 一个可迭代(iterable)是实现了IntoIterator的任何类型，可以通过调用into_iter方法得到迭代器(iterator)。
        - 迭代器生产值。
        - 迭代器生产的值是items。 
        - 接收迭代器生成项目的代码是消费者？？？？？

## 第 087 个番茄时间

    时间：2022.02.24 00:41
    内容：《Programming Rust 2nd Edition》第348-350页。
        [Creating Iterators]
        大部分集合类型提供iter()和iter_mut()以生成迭代器。
        ```
        let v = vec![4, 20, 12, 8, 6];
        let mut iterator = v.iter();
        assert_eq!(iterator.next(), Some(&4));
        ```
        无论是否合理，每一种类型都是可以实现iter()和iter_mut()的。
        对于有多种常用迭代方案的类型，通常会提供多种迭代方案。 比如&str string slice，.bytes()生成字节(byte)，.chars()生成字符(Unicode字符)。

## 第 088 个番茄时间

    时间：2022.03.01 01:25
    内容：《Programming Rust 2nd Edition》第350-353页。
        [IntoIterator Implementations]
        三种不同的IntoIterator实现：
            (&favorites).into_iter()
            (&mut vector).into_iter()
            favorites.into_iter()
        迭代器的一般原则是：高效和可预测。

         [from_fn and successors]
        通过函数/闭包直接返回迭代器。 

        [drain Methods]
        drain() 和 into_iter() 具有类似功能，区别点在于drain()不消费原集合？？？  

## 第 089 个番茄时间

    时间：2022.03.01 10:41
    内容：《Programming Rust 2nd Edition》第354-357页。
        [Other Iterator Sources]

        [Iterator Adapters] 迭代器适配器？
        map adapter: 用闭包作用于各条目。
        filter adapter: 用闭包去筛选条目。
        ```
        let text = " ponies \n giraffes\niguanas \nsquid".to_string();
        let v: Vec<&str> = text.lines()
            .map(str::trim)
            .filter(|s| *s != "iguanas")
            .collect();
        assert_eq!(v, ["ponies", "giraffes", "squid"]);
        ```

## 第 090 个番茄时间

    时间：2022.03.02 10:12
    内容：《Programming Rust 2nd Edition》第357-359页。
        关于迭代适配器，有两个要点需要注意：
        第一，只在迭代器上调用适配器不会消耗任何条目；它只会返回一个新的迭代器，根据需要从第一个迭代器中提取即可生成新条目。在适配器链中，真正完成工作的唯一方法是在最终迭代器上调用next()。
        
        第二，迭代器适配器是一个零开销抽象。由于map,filter及其同伴是泛型的，将它们应用于迭代器会专门针对所涉及的特定迭代器类型进行代码实现。

        [filter_map and flat_map]
        filter_map 类似于 filter 与 map 的结合。

## 第 091 个番茄时间

    时间：2022.03.03 10:20
    内容：《Programming Rust 2nd Edition》第359-361页。
        ```
        text.split_whitespace().filter_map(|w| f64::from_str(w).ok())
        --------------------
        text.split_whitespace().map(|w|f64::from_str(w)).filter(|r|r.is_ok()).map(|r|r.unwrap())
        ```
        传递到flat_map的闭包必须是可迭代的(iterable)。

        事实上，由于Option是一个可迭代的，行为类似于 zero 或一个条目的序列；如果closure返回一个Option<T>，那么iterator.filter_map(closure)相当于iterator.flat_map(closure)。 ？？？？
        相当于把多个loop打包成一个迭代器使用？

## 第 092 个番茄时间

    时间：2022.03.03 19:45
    内容：《Programming Rust 2nd Edition》第361-364页。
        [flatten] 扁平化～～～
        用于把二级集合整合为一维集合。
        ```
        fn flatten(self) -> impl Iterator<Item=Self::Item::Item>
            where Self::Item: IntoIterator;
        ```
        flat_map() 相当于 map().flatten()。

        [take and take_while]   满足条件 --> 取用

        [skip and skip_while]   满足条件 --> 丢弃

## 第 093 个番茄时间

    时间：2022.03.06 01:44
    内容：《Programming Rust 2nd Edition》第364-366页。
        [peekable] Peekable 迭代器
        所有的iterator可以转换成peekable iterator。
        先通过.peek()判断是否存在下一个条目，再执行.next()。

        [fuse]
        用于确保迭代器产生一次 None 之后，后续.next()永远产生 None。 

        ----------------

        [Reversible Iterators and rev] 迭代器翻转，rev适配器。 
        通过实现std::iter::DoubleEndedIterator trait来实现双向迭代。
        ```
        let bee_parts = ["head", "thorax", "abdomen"];
        let mut iter = bee_parts.iter();

        assert_eq!(iter.next(),      Some(&"head"));
        assert_eq!(iter.next_back(), Some(&"abdomen"));
        assert_eq!(iter.next(),      Some(&"thorax"));
        assert_eq!(iter.next_back(), None);
        assert_eq!(iter.next(),      None);
        ```

## 第 094 个番茄时间

    时间：2022.03.06 14:48
    内容：《Programming Rust 2nd Edition》第367-369页。
        并非所有的迭代器都能实现DoubleEndedIterator，比如流数据？io？

       [Iterator Adapters] - [inspect] 
       多用于测试代码中的调试管道，通常进行打印、断言操作。
       ```
        let upper_case: String = "große".chars()
            .inspect(|c| println!("before: {:?}", c))
            .flat_map(|c| c.to_uppercase())
            .inspect(|c| println!(" after: {:?}", c))
            .collect();
        assert_eq!(upper_case, "GROSSE");
       ```

       [Iterator Adapters] - [chain]
       迭代器合并

## 第 095 个番茄时间

    时间：2022.03.06 16:02
    内容：《Programming Rust 2nd Edition》第369-371页。
       [Iterator Adapters] - [enumerate]
       返回(key, value)对。

       [Iterator Adapters] - [zip] 
       如拉链一样，一一组合？？？
       ```
       let v: Vec<_> = (0..).zip("ABCD".chars()).collect();
       assert_eq!(v, vec![(0, 'A'), (1, 'B'), (2, 'C'), (3, 'D')]);
       ```

       [Iterator Adapters] - [by_ref]
       借用迭代器，而非消费。
       注意：但是具体的item被消费掉了。   ？？？

       ```
        let mut words = vec!["hello", "world", "of", "Rust"].into_iter();

        // 以前两个单词为例。
        let hello_world: Vec<_> = words.by_ref().take(2).collect();
        assert_eq!(hello_world, vec!["hello", "world"]);

        // 收集剩下的单词。
        // 我们只能这样做，因为我们之前使用了 `by_ref`。
        let of_rust: Vec<_> = words.collect();
        assert_eq!(of_rust, vec!["of", "Rust"]);
       ```

## 第 096 个番茄时间

    时间：2022.03.06 16:59
    内容：《Programming Rust 2nd Edition》第371-页。
       [Iterator Adapters] - [cloned,copied]
       iter_a.cloned()  类似  iter_a.map(|item| item.clone())   
       iter_a.copied()  类似  iter_a.map(|r| *r)

       [Iterator Adapters] - [cycle]
       无限重复迭代器。 迭代器需要实现std::clone::Clone。

## 第 097 个番茄时间

    时间：2022.03.07 00:13
    内容：《Programming Rust 2nd Edition》第373-374页。
        [Consuming Iterators] - Simple Accumulation: count, sum, product
        .count()    统计
        .sum()      求和
        .product()  阶乘？？？

        [Consuming Iterators] - max, min
        使用std库自带的比较函数。浮点类型未实现std::cmp::Ord，所以不能使用max和min。

        [Consuming Iterators] - max_by, min_by
        使用自定义的比较函数。
        这两个方法以引用的方式传递条目到比较函数中。

## 第 098 个番茄时间

    时间：2022.03.07 21:57
    内容：《Programming Rust 2nd Edition》第375-377页。
        [Consuming Iterators] - max_by_key, min_by_key
        max_by传入的是比较函数，
        max_by_key传入的是值提取，

        [Consuming Iterators] - any and all
        传入闭包，作为取舍的判断。
        any 满足判断条件的任意一个
        all 满足判断条件的所有

        [Consuming Iterators] - position, rposition, and ExactSizeIterator
        position    返回第一个满足条件的条目的序号。
        rposition   position的反向。。。  需要可翻转的迭代器，同时需要实现std::iter::ExactSizeIterator。

## 第 099 个番茄时间

    时间：2022.03.08 01:25
    内容：《Programming Rust 2nd Edition》第377-379页。
        [Consuming Iterators] - fold and rfold
        前一次迭代的输出值作为下一次迭代的输入值。
        ```
        leta=[5,6,7,8,9,10];
        assert_eq!(a.iter().fold(0, |n, _| n+1), 6);        // .count()
        assert_eq!(a.iter().fold(0, |n, i| n+i), 45);       // .sum()
        assert_eq!(a.iter().fold(1, |n, i| n*i), 151200);   // .product()
        
        // max
        assert_eq!(a.iter().cloned().fold(i32::min_value(), std::cmp::max), 10);
        ```

        [Consuming Iterators] - try_fold and try_rfold
        ```
        use std::error::Error;
        use std::io::prelude::*;
        use std::str::FromStr;
        fn main() -> Result<(), Box<dyn Error>> {
            let stdin = std::io::stdin();
            let sum = stdin.lock()
                .lines()
                .try_fold(0, |sum, line| -> Result<u64, Box<dyn Error>> {
                    Ok(sum + u64::from_str(&line?.trim())?)
                })?;
            println!("{}", sum);
            Ok(())
        }
        ```
        Box<dyn Error> 知识点又忘了。。。。   FUCK

## 第 100 个番茄时间

    时间：2022.03.08 22:00
    内容：《Programming Rust 2nd Edition》第379-381页。
        [Consuming Iterators] - nth, nth_back
        .nth(n)  后续迭代序列的第n个。 
        .nth(0)即为.next()。
        .nth_back(0)即为.next_back()。

        [Consuming Iterators] - last
        最后一个迭代值，注意该方法会消费所有的item。对于可翻转迭代器，可以使用.next_back()。

        [Consuming Iterators] - find, rfind, and find_map
        查找满足条件(闭包)的条目。
        
        .find_map() ???

## 第 101 个番茄时间

    时间：2022.03.09 00:58
    内容：《Programming Rust 2nd Edition》第381-385页。
        [Consuming Iterators] - Building Collections: collect and FromIterator ？？？
        实现了FromIterator trait的类型可以直接在相应的iterator上执行.collect()来生成集合。？？？
        from_iter() 

        [Consuming Iterators] - The Extend Trait
        用于扩展已存在的集合，集合整合/拼接/合并。

        [Consuming Iterators] - partition
        分割迭代器，通过传入的闭包来判断。 ？？？

        [Consuming Iterators] - for_each and try_for_each
        .for_each() 只是简单的将闭包应用到各个条目。
        跟.inspect()很像，也许不同点在于：.for_each()消费迭代器？？？

        .try_for_each() ： 执行闭包可能出错时使用。

## 第 102 个番茄时间

    时间：2022.03.09 02:52
    内容：《Programming Rust 2nd Edition》第385-386页。
        [Implementing Your Own Iterators]
        通过实现IntoIterator和Iterator traits，从而自定义迭代器。

## 第 103 个番茄时间

    时间：2022.03.09 11:19
    内容：《Programming Rust 2nd Edition》第386-389页。
        [Implementing Your Own Iterators]
        为BinaryTree<T>实现迭代。
        迭代二叉树！！！   ？？？   没搞懂～

## 第 104 个番茄时间

    时间：2022.03.12 19:36
    内容：《Programming Rust 2nd Edition》第391-394页。
        [CHAPTER 16 -- Collections]
        
        Vec<T>

        vector的长度和索引是usize类型，其它类型均报错。

## 第 105 个番茄时间

    时间：2022.03.13 00:03
    内容：《Programming Rust 2nd Edition》第395-397页。
        array, slice, vector 都有 .iter() .iter_mut() .first() .last() .get() .first_mut() .last_mut() .get_mut(index)方法。

        [Growing and Shrinking Vectors] 向量的扩增和瘦身。

## 第 106 个番茄时间

    时间：2022.03.13 02:59
    内容：《Programming Rust 2nd Edition》第398-400页。
        vec.resize(new_len, value)
        vec.resize_with(new_len, closure)
        vec.truncate(new_len)
        vec.clear()  == vec.truncate(0)
        vec.extend(iterable)                    // 类似于多次 .push() 操作。
        vec.split_off(index)                    // 相比于 vec.truncate(index)，该方法还会返回被移除部分的值。
        vec.append(&mut vec2)                   // 相对于vec.extend(vec2)，该方法消费了vec2，执行结束后，vec2是空的。
        vec.drain(range)                        // 移出某个范围的元素作为返回值。
        vec.retain(test)                        // 按条件(test: 闭包或者函数)移出某些元素作为返回值。除了性能差异外，其效果类似于： vec = vec.into_iter().filter(test).collect();
        vec.dedup()                             // 移除重复的相邻元素。
        vec.dedup_by(same)                      // 移除重复的相邻元素，用函数或闭包来判断是否相等。
        vec.dedup_by_key(key)                   // 移除重复的相邻元素，以 key(&mut elem1) == key(&mut elem2) 作为判断。

## 第 107 个番茄时间

    时间：2022.03.13 11:37
    内容：《Programming Rust 2nd Edition》第400-403页。
        slices.concat()
        slices.join(&separator)
        slice.iter(), slice.iter_mut()
        slice.split_at(index), slice.split_at_mut(index)
        slice.split_first(), slice.split_first_mut()
        slice.split_last(), slice.split_last_mut()
        slice.split(is_sep), slice.split_mut(is_sep)
        slice.rsplit(is_sep), slice.rsplit_mut(is_sep)
        slice.splitn(n, is_sep), slice.splitn_mut(n, is_sep)
        slice.rsplitn(n, is_sep), slice.rsplitn_mut(n, is_sep)
        slice.chunks(n), slice.chunks_mut(n)
        slice.rchunks(n), slice.rchunks_mut(n)
        slice.chunks_exact(n), slice.chunks_exact_mut(n)
        slice.rchunks_exact(n), slice.rchunks_exact_mut(n)
        slice.windows(n)

## 第 108 个番茄时间

    时间：2022.03.13 14:43
    内容：《Programming Rust 2nd Edition》第403-405页。
        slice.swap(i, j)            // 交换元素。
        slice_a.swap(&mut slice_b)  // slice_a, slice_b 长度相同。
        vec.swap_remove(i)          // 移除某元素，然后用尾部元素填充空位。 

        ------------- 排序 搜索
        slice.sort()
    slice.sort_by(cmp)              // cmp: Fn(&T, &T) -> std::cmp::Ordering   指定排列顺序。
        ```
        students.sort_by(|a, b| a.last_name.cmp(&b.last_name));
        -------
        students.sort_by(|a, b| {
            let a_key = (&a.last_name, &a.first_name);
            let b_key = (&b.last_name, &b.first_name);
            a_key.cmp(&b_key)
        });
        ```
    slice.sort_by_key(key)      // key: Fn(&T) -> K where K: Ord   按key升序排列。
    slice.reverse()
    
    slice.binary_search(&value), slice.binary_search_by(&value, cmp),
    slice.binary_search_by_key(&value, key)
    slice.contains(&value)
    slice.iter().position(|x| *x == value)

## 第 109 个番茄时间

    时间：2022.03.13 15:29
    内容：《Programming Rust 2nd Edition》第406-410页。
        如果T实现了PartialEq trait，那么array<T>,slice<T>,vec<T> 也同步实现了PartialEq trait。亦即可直接比较。
        slice.starts_with(other)
        slice.ends_with(other)

        ```
        assert_eq!([1, 2, 3, 4].starts_with(&[1, 2]), true);
        assert_eq!([1, 2, 3, 4].starts_with(&[2, 3]), false);

        assert_eq!([1, 2, 3, 4].ends_with(&[3, 4]), true);
        ```
        随机取数：
        slice.choose(&mut rng)      // 随机选一个元素
        slice.shuffle(&mut rng)     // 随机重新排序
        ```
        use rand::seq::SliceRandom;
        use rand::thread_rng;
        my_vec.shuffle(&mut thread_rng());
        ```
        Rust不会发生“无效”错误。
        
        [VecDeque<T>]  'deque' -- double ended queue
        VecDeque是环形buffer的一种实现；相比于Vec<T>，非常适合FIFO场景。 

        deque.push_front(value)
        deque.push_back(value)
        deque.pop_front()
        deque.pop_back()
        deque.front(), deque.back()  类似于 vec.first(), vec.last()
        deque.front_mut(), deque.back_mut()

        deque.make_contiguous()  // 重整序列。

        Vec<T>和VecDeque<T>可以相互转换：
        Vec::from(deque)
        VecDeque::from(vec)

## 第 110 个番茄时间

    时间：2022.03.13 16:06
    内容：《Programming Rust 2nd Edition》第410-411页。
        [BinaryHeap<T>] 二叉堆，最大值总是在队列最前面。
        要求T类型实现了 Ord trait。

        heap.push(value)
        heap.pop()          // 提取最大值
        heap.peek()         // 借用最大值
        heap.peek_mut()     // 可变借用最大值？？？？

        特别适合用来作为有优先级的任务堆。
        ```
        while let Some(task) = heap.pop() {
            handle(task);
        }
        ```

## 第 111 个番茄时间

    时间：2022.03.13 17:21
    内容：《Programming Rust 2nd Edition》第411-415页。
        [HashMap<K, V> and BTreeMap<K, V>]
        HashMap<K, V>存储在table中，K需要实现Hash 和 Eq trait。本质上以hash(T)作为主键。
        BTreeMap<K, V>存储在nodes中，是有序的，K需要实现Ord trait。K作为主键。

        B-trees效率比balanced binary trees(平衡二叉树)高。

        HashMap::new(), BTreeMap::new()
        iter.collect()   // item: Iterator<Item=(K, V)>
        HashMap::with_capacity(n)

        map.len()
        map.is_empty()
        map.contains_key(&key)
        map.get(&key)
        map.get_mut(&key)
        map.insert(key, value)
        map.extend(iterable)
        map.append(&mut map2)  // 移动map2中所有实体到map中
        map.remove(&key)        // 删除某实体，返回Option<V>
        map.remove_entry(&key)  // 删除某实体，返回Option<(K, V)>
        map.retain(test)        // 
        map.clear()
        btree_map.split_off(&key)   

        other: 【译】为什么Rust中的BTreeMap没有with_capacity()方法？ 
                https://juejin.cn/post/6904621455724511245

## 第 112 个番茄时间

    时间：2022.03.14 22:10
    内容：《Programming Rust 2nd Edition》第415-418页。
        map.entry(key).or_insert(value)     // mut引用 已有或新建的实体
        map.entry(key).or_default()
        map.entry(key).or_insert_with(default_fn)
        map.entry(key).and_modify(closure)

        (for (k, v) in map)  ----->  (K, V)
        (for (k, v) in &map) ----->  (&K, &V)
        (for (k, v) in &mut map) -----> (&K, &mut V)

        map.keys()      ----->  &K
        map.values()    ----->  &V
        map.values_mut()----->  &mut V

## 第 113 个番茄时间

    时间：2022.03.15 01:26
    内容：《Programming Rust 2nd Edition》第418-421页。
        HashSet<T> and BTreeSet<T>
        即 HashMap<T, ()> 和 BTreeMap<T, ()>

        HashSet::new(), BTreeSet::new()
        iter.collect()
        HashSet::with_capacity(n)
        set.len()
        set.is_empty()
        set.contains(&value)    // value 即 key
        set.insert(value)
        set.remove(&value)
        set.retain(test)

        不能以可变引用的方式迭代set(集合)，因为无法获取存储在集合中的值的mut引用。

        set.iter()


        set.get(&value)
        set.take(&value)
        set.replace(value)

        set1.intersection(&set2)        // 取集合的交集
        set1.union(&set2)               // 并集
        set1.difference(&set2)          // 在set1中，不在set2中
        set1.symmetric_difference(&set2) // 对称差集，在set1或set2中，但不在两者交集中。
        set1.is_disjoint(set2)          // 判断是否无任何交集
        set1.is_subset(set2)            // set1是否为set2的子集
        set1.is_superset(set2)          // set1是否为set2的超集。

        支持 == 和 != 运算符

## 第 114 个番茄时间

    时间：2022.03.15 10:34
    内容：《Programming Rust 2nd Edition》第422-425页。
        [Hashing] std::hash::Hash trait
        大部分实现Eq的内建类型同样实现了Hash。
        Hash标准库有一个原则：无论是指向引用还是值，具有相同的hash值。 所以：hash(&T) == hash(T) ？？？

        [Using a Custom Hashing Algorithm]
        rust默认的hash算法是；SipHash-1-3。  SipHash 能够有效减缓 hash flooding 攻击。凭借这一点，它逐渐成为 Ruby、Python、Rust 等语言默认的 hash 表实现的一部分。

        可以使用其它hash算法。

        [Beyond the Standard Collections]


## 第 115 个番茄时间

    时间：2022.03.16 01:52
    内容：《Rust 程序设计》p319-p324,相当于《Programming Rust 2nd Edition》第427-435页。
        [CHAPTER 17 -- Strings and Text]  
        String实际上是Vec<u8>的包装类型，同时确保了vec内容始终是良好的UTF-8格式。所以String与Vec性能相同。

## 第 116 个番茄时间

    时间：2022.03.17 00:24
    内容：《Rust 程序设计》p325-p328，17.3.7
    slice.to_string() == &slice.to_owned() ？？？

## 第 117 个番茄时间

    时间：2022.03.18 00:28
    内容：《Rust 程序设计》p328-334，17.3.15
        对于一个实现了Display特性的类型，标准库自动为其实现std::str::ToString 特性。

        String::from_urf8_lossy(byte_slice) ？？？   返回值：Cow<str> ？？？

## 第 118 个番茄时间

    时间：2022.03.20 02:31
    内容：《Rust 程序设计》p335-p335，17.3.16
        Cow类型可以同时处理(存储) Owned 和 Borrowed 数据。
        对于纠结String类型还是&str类型的变量改用Cow智能指针类型。 ？？？ 比如“同时接受 &str 和 String 作为参数”的场景～～～

        无论是Owned还是Borrowed，Cow<'a T>均生成&T以供使用。
        ```
        use std::borrow::Cow;

        fn get_name() -> Cow<'static, str> {
            std::env::var("USER")
                .map(|v| Cow::Owned(v))
                .unwrap_or(Cow::Borrowed("whoever you are"))
        }
        ```

## 第 119 个番茄时间

    时间：2022.03.20 23:54
    内容：《Rust 程序设计》p335-p338，next: 17.4.1
        因为Cow<'a, str> 提供了来自String和&str的From和Into转换，因此可以简化代码：
        ```
        fn get_name() -> Cow<'static, str> {
            std::env::var("USER")
            .map(|v| v.into())
            .unwrap_or("whoever you are".into())
        }
        ```
        因为Cow<'a, str>实现了 std::ops::Add 和 std::ops::AddAssign，所以：
        ```
        if let Some(title) = get_title() {
            name += ", ";
            name += title;
        }
        ```

## 第 120 个番茄时间

    时间：2022.03.24 22:01
    内容：《Rust 程序设计》p338-343，Next: Ch17.4.8
        格式化形式参数：{which:how}，which用以标注参数名或者参数序号，how用以标注格式化要求。 

        格式化文本值时，模版字符串`{:*^m.n}`，`*` 是填充字符，`^`或`<`或`>` 是对齐方式，m 是最小字段宽度，n 是最大文本长度。
        Table 17-5. Format string directives for text  

        Table 17-6. Format string directives for integers

        Table 17-7. Format string directives for floating-point numbers
        
        {:?} 和 {:#?}

        {:p}    格式化指针(pointer)

        ```
         assert_eq!(format!("{mode} {2} {} {}",
                       "people", "eater", "purple", mode="flying"),
                        "flying purple people eater");
        ```

        动态宽度和精度：
        ```
        format!("{:>1$}", content, get_width())
        ----------
        format!("{:>width$.limit$}", content,
            width=get_width(), limit=get_limit())

        ----------
        format!("{:.*}", get_limit(), content)
        ```

## 第 121 个番茄时间

    时间：2022.03.25 00:55
    内容：《Rust 程序设计》p344-347，Next: Ch17.5.1
        可以通过实现std::fmt模块中的某些trait可以自定义格式化类型。
        Table 17-8. Format string directive notation

        使用格式化语言？
        ```
        macro_rules! log { // no ! needed after name in macro definitions 
            ($format:tt, $($arg:expr),*) => (
                write_log_entry(format_args!($format, $($arg),*))
            )
        }
        ```
        正则表达式包regex不在std中，但仍旧是rust团队维护的。

## 第 122 个番茄时间

    时间：2022.03.26 
    内容：《Rust 程序设计》p347-p351，Next: 第18章 -- 输入和输出

        正则表达式。。。。

        lazy_static是个好东西。。。。
        ```
        use lazy_static::lazy_static;

        lazy_static! {
            static ref SEMVER: Regex
                = Regex::new(r"(\d+)\.(\d+)\.(\d+)(-[-.[:alnum:]]*)?")
                    .expect("error parsing regex");
        }
        ```
        如上代码中的SEMVER并非Regex类型，而是一个宏生成的实现了Deref<Target=Regex>的类型，具备与Regex完全相同的方式。首次deref SEMVER的时候，执行初始化，随后被保存起来随时取用。

        规划化形式：
            - Unicode NFC (规范化形式C)  -- 最大化组合
            - Unicode NFD (规范化形式D)  -- 最大化分解
            - NFKC
            - NFKD

        crate: unicode-normalization

        规范化形式通常适合持久存储，而不受Unicode标准演进的影响。

## 第 123 个番茄时间

    时间：2022.03.26 17:27 
    内容：《Rust 程序设计》p352-356，Next: Ch18.1.3
        Reader & Writer
        reader.read(&mut buffer)
        reader.read_to_end(&mut byte_vec)
        reader.read_to_string(&mut string)
        reader.read_exact(&mut buf)

        reader.bytes()
        reader.chain(reader2)
        reader.take(n)

        如下方法需要reader实现BufRead：
        reader.read_line(&mut line)
        reader.lines()
        reader.read_until(stop_byte, &mut byte_vec), reader.split(stop_byte)

## 第 124 个番茄时间

    时间：2022.03.26 20:42
    内容：《Rust 程序设计》p356-p359，Next: Ch18.1.5

        let lines = reader.lines().collect::<io::Result<Vec<String>>>()?; 略懵。。。
        ```
        impl<T, E, C> FromIterator<Result<T, E>> for Result<C, E>
            where C: FromIterator<T>
            {
            ...
            }
        ```
        假设 C 是任何集合类型，如 Vec 或 HashSet。 只要我们已经知道如何从 T 值的迭代器构建 C，我们就可以从产生 Result<T, E> 值的迭代器构建 Result<C, E>。 
        
        reader.lines()可迭代生成String，
        T: IntoIterator<Item=String>  
        String                  ==>     C: Vec<String>
        Result<T, E>            ==>     Result<C, E>
        io::Result<String>      ==>     io::Result<Vec<String>>

        ?????

## 第 125 个番茄时间

    时间：2022.03.27 21:54
    内容：《Rust 程序设计》p359-361，Next: Ch18.1.8
        写入器：Writer
        writer.write(&buf)      // 底层方法，一般不建议直接使用。
        writer.write_all(&buf)
        writer.flush()

        添加缓冲：   
            BufReader::new(reader)
            BufWriter::with_capacity(size, writer)

        文件
        File::open(filename)		reader
        File::create(filename)		新建文件，如果存在则覆盖。
        
		如果上述两种方式不满足需求，则通过OpenOptions指定具体行为。
			- .append()
			- .write()
			- .create_new()
		构建器???  builder ???

		Seek特征

		file.seek(SeekFrom::Start(0))		定位到文档开头
		file.seek(SeekFrom::Current(-8))	当前位置倒退8字节。

## 第 126 个番茄时间

    时间：2022.03.27 23:28
    内容：《Rust 程序设计》p361-364，Next: Ch18.2
		io::stdin()		Stdin有一个.lock()方法用于获取互斥量并返回io::StdinLock()，由于技术原因，不能直接使用io::stdin().lock()，而应当有一个中间变量，以保存生命周期信息。
		io::stdout()
		io::stderr()
		Cursor::new(buf)	Cursor实现了Read,BufRead,Seek，对于可写buf(如：&mut [u8], Vec<u8>)还实现了Write。
		std::net::TcpStream		网络连接，双向通道。
		std::process::Command

		std::sink()		无操作写入器，所有数据被抛弃，直接返回Ok。
		std::empty()	无操作读取器，读取成功，但没有数据(返回 end-of-input)。
		std::repeat(byte)	无止尽的返回byte。

		二进制数据、压缩、序列化。
		byteorder crate
		flate2 crate
		serde crate

## 第 127 个番茄时间

    时间：2022.03.28 00:42
    内容：《Rust 程序设计》p364-p370，Next: Ch18.3 网络编程
        操作文件及目录
		OsStr是UTF-8的超集，可能不是有效的Unicode。用于在系统中表示路径、文件名、参数等信息。
		Path跟OsStr是一样的，只是多了几个处理文件名的方式。
		
		Table 18-1. Filename types

		str		==>		String
		OsStr	==>		std::ffi::OsString
		Path	==>		std::path:PathBuf

		如上三种类型均实现了AsRef<Path>，因此可以作为方法中的泛型参数，，， （这种表述方法？？？）
		
		呵，AsRef 又忘了。。。。。。。。。   M Fuck....

		Path::new(str)	将&str和&OsStr转化为&Path。
		path.parent()
		path.file_name()
		path.is_absolute(), path.is_relative()
		path1.join(path2)
		path.components()
		path.ancestors()
		path.to_str()
		path.to_string_lossy()		返回std::borrow::Cow<str>
		path.display()

		Table 18-2. Summary of filesystem access functions	std::fs

		读取目录，std::fs::DirEntry类型的一些方式：
			.file_name()
			.path()			返回全新的PathBuf。
			.file_type()	返回io::Result<FileType>
			.metadata()		

		`#[cfg]`属性表示“条件编译”
		```
		#[cfg(unix)]
		use std::os::unix::fs::symlink;
    
		/// Stub implementation of `symlink` for platforms that don't provide it.
    	#[cfg(not(unix))]
		fn symlink<P: AsRef<Path>, Q: AsRef<Path>>(src: P, _dst: Q) -> std::io::Result<()>
    	{
        	Err(io::Error::new(io::ErrorKind::Other,
                           format!("can't copy symbolic link: {}",
                                   src.as_ref().display())))
		}

		```
		
## 第 128 个番茄时间

    时间：2022.03.28 01:43
    内容：《Rust 程序设计》p370-p374, 第19章：并发。
		吐槽：中文版的翻译真是有够恶心的。

		有用reqwest来写demo。
		
		-------------------------
		使用Rust线程的3种方式：
		- Fork-join parallelism    	并行的飞叉-合并
		- Channels					通道
		- Shared mutable state		共享的可修改状态

		Rust的所有权、借用、生命周期等一系列知识在“并发”中将统统被使用。
		
## 第 129 个番茄时间

    时间：2022.03.28 21:53
    内容：《Rust 程序设计》p374-p380, Next: Ch19.1.4 Rayon??? 
		生成新线程：std::thread::spawn
		Rust中的新线程是一个真实的系统线程，有自己的栈。

		使用引用计数器的并发版本：原子引用计数器Arc 来跨线程共享不可修改的数据。

## 第 130 个番茄时间

    时间：2022.03.28 22:42
    内容：《Rust 程序设计》pp380-p383, Next: Ch19.2 通道。
		标准库中的spawn函数是一个重要的原语，但并不是专门为并行Fork-Join设计的。基于spawn的crossbeam库受限线程(scoped thread)可以相当自然的支持并行fork-join。
		除了Crossbeam，Rayon库实现了并发任务。
		```
		use rayon::prelude::*;
		// "do 2 things in parallel"
		let (v1, v2) = rayon::join(fn1, fn2);
	
		// "do N things in parallel"  N 为CPU核心数
		giant_vector.par_iter().for_each(|value| {
			do_thing_with_value(value);
		});
		```
		MapReduce编程模型？？？
		
		Rayon使用work-stealing技术实现在线程间负载均衡。

## 第 131 个番茄时间

    时间：2022.03.29 22:05
    内容：《Rust 程序设计》pp383-387, Next:Ch19.2.2
		[19.2 通道channel]
		channel 是把数据从一个线程发送到另一个线程的单向管道 -- 一个线程安全的队列 -- 线程间转移数据所有权。

		channel 属于 std::sync::mpsc模块

## 第 132 个番茄时间

    时间：2022.03.30 00:10
    内容：《Rust 程序设计》pp387-p391, Next:Ch19.2.5
		mpsc ：multi-producer, signle-consumer
		所以一个channel可以接收多个发送者。
		Sender<T>实现了Clone trait，需要额外的Sender时，只需要进行Clone即可。

		PS：Receiver<T>不能clone，如果需要多个线程从同一个channel接收数据，则需要使用Mutex。

		同步通道    
		```
		use std::sync::mpsc::sync_channel;
		let (sender, receiver) = sync_channel(1000);		
		```

## 第 133 个番茄时间

    时间：2022.03.30 01:12
    内容：《Rust 程序设计》p391-p395, Next:Ch19.3
		std::marker::Send	数据在线程间安全的转移。
		std::marker::Sync	数据在线程间安全的共享。
		安全：没有数据争用和其他未定义行为。
		
		大多数的类型同时实现了Send和Sync。

		少数没有实现Send和Sync的类型主要用于在非线程安全的条件下提供可修改能力，例如：std::rc::Rc<T>如果在两个线程中同时clone，可能出现数据争用。

		.off_thread()	？？？

		通道channel还可以用于异步服务。。。。

		Next： 19.3 共享的可修改状态。
		
## 第 134 个番茄时间

    时间：2022.03.30 22:06
    内容：《Rust 程序设计》p395-p398, Next:Ch19.3.3
		互斥量(mutex)或锁(lock)用于独占特定数据的访问权。

		Arc和Mutex经常一起使用，使用Arc进行跨线程共享数据，使用Mutex进行跨线程共享可修改数据。

		对于Mutex类型的数据，操作数据的唯一方式是先调用.lock()方法。
		```
		let mut guard = self.waiting_list.lock().unwrap();
		```
		.lock()方法返回的MutexGuard<WaitingList>值是对&mut WaitingList的一个封装。 因为实现了Deref，所以可以直接调用 T 的方法。

		获取到互斥量的变量释放时，锁也被释放。

## 第 135 个番茄时间

    时间：2022.03.30 23:44
    内容：《Rust 程序设计》p398-p400, Next:Ch19.3.7
		在Rust中，&mut 表示专属访问/排他性访问(exclusive access), & 表示共享访问(shared access)。
		一般情况下，如果父线程中没有专属访问权，那么在子线程中也没有。 但Mutex可以通过锁来实现。

		Mutex的内部修改能力与RefCell相同，都是由Rust编译器来保障的。

		Mutex可能存在的问题：
			- Rust程序可以不出现数据竞争，但可能出现竞态条件(race condition)。
			- 共享的可修改状态可能影响程序设计。？？？？
			- 其他问题？？？？？    。。。。。

		尽量使用结构化处理方式，其次再考虑Mutex。  ？？？？

		死锁	Deadlock
		中毒的互斥量	Poisoned Mutexes
	
## 第 136 个番茄时间

    时间：2022.03.31 00:51
    内容：《Rust 程序设计》p400-p402, Next:Ch19.3.9
		Rust channel 是多生产者单消费者的 -- 一个通道只有一个Receiver。 通过Mutex可以实现Receiver共享。

		```
        pub mod shared_channel {
            use std::sync::{Arc, Mutex};
            use std::sync::mpsc::{channel, Sender, Receiver};
            
            /// A thread-safe wrapper around a `Receiver`.
            #[derive(Clone)]
            pub struct SharedReceiver<T>(Arc<Mutex<Receiver<T>>>); 
            
            impl<T> Iterator for SharedReceiver<T> {
                type Item = T;
                /// Get the next item from the wrapped receiver.
                fn next(&mut self) -> Option<T> {
                        let guard = self.0.lock().unwrap(); guard.recv().ok()
                } 
            }

            /// Create a new channel whose receiver can be shared across threads.
            /// This returns a sender and a receiver, just like the stdlib's
            /// `channel()`, and sometimes works as a drop-in replacement. 
            pub fn shared_channel<T>() -> (Sender<T>, SharedReceiver<T>) {
                let (sender, receiver) = channel();
                (sender, SharedReceiver(Arc::new(Mutex::new(receiver))))
            }
        }
        ```

        读写锁 RWLock
        通常可以用在APP对配置文件的读写上。？？？   实现一个写入器和多个读取器。
        重新加载配置文件时使用RWLock::write()，防止读取过程中数据变动？？？
        ```
        fn reload_config(&self) -> io::Result<()> {
            let new_config = AppConfig::load()?;
            let mut config_guard = self.config.write().unwrap();
            *config_guard = new_config;     // 这里令人困惑。。。。。。？？？？？？？
            Ok(())
        }
        ```

## 第 137 个番茄时间

    时间：2022.04.03 15:20
    内容：《Rust 程序设计》p402-p404, Next:Ch19.3.11
		std::sync::Condvar 类型实现了条件变量(condition variable)。   ？？？？

		std::sync::atomic 模块包含无锁并发编程要使用的原子类型。多线程同时读取原子类型数据不会造成数据争用。
        
        原子类型可用于子线程的取消指令。（主线程写标识，子线程读标识）。 相比于Mutex<bool>或channel实现方式，原子操作更高效，通常只是一个CPU指令即可。


## 第 138 个番茄时间

    时间：2022.04.03 17:14
    内容：《Programming Rust 2nd Edition》第535-538页。
        全局变量  Global Variables

        static PACKETS_SERVED: usize = 0;    // 不可修改

        搞成原子整数(atomic integer)即可线程安全的进行读写。 
        ```
        use std::sync::atomic::AtomicUsize;
        use std::sync::atomic::Ordering;

        static PACKETS_SERVED: AtomicUsize = AtomicUsize::new(0);
        PACKETS_SERVED.fetch_add(1, Ordering::SeqCst);
        ```
        原子全局变量只能存储一个整数或者布尔。
        
        若要创建其他类型的全局变量：
            - 变量必须满足线程安全：安全的静态变量必须同时Sync且non-mut。？？？？
            - 静态初始化器只能调用专门标记为const的函数？？？？？

        lazy_static crate ～～～

        ```
        use lazy_static::lazy_static;
        use std::sync::Mutex;
        
        lazy_static! {
            static ref HOSTNAME: Mutex<String> = Mutex::new(String::new());
        }
        ```
        
        const 与 static 区别？？？？

## 第 139 个番茄时间

    时间：2022.04.04 15:56
    内容：《Programming Rust 2nd Edition》第539-541页。
        [CHAPTER 20 -- Asynchronous Programming]
        异步任务(asynchronous tasks)类似于线程，但更高效且节省资源。   so，异步任务本质是线程池？？？？
        ```rust
        // use std::{net, thread};
        use async_std::{net, task};

        let listener = net::TcpListener::bind(address).await?;
        let mut new_connections = listener.incoming();

        // for socket_result in listener.incoming() {
        while let Some(socket_result) = new_connections.next().await {
            let socket = socket_result?;
            let groups = chat_group_table.clone();

            // thread::spawn(|| {
            //     log_error(serve(socket, groups));
            // });
            task::spawn(async {
                        log_error(serve(socket, groups).await);
                    });
        }
        ```

## 第 140 个番茄时间

    时间：2022.04.04 16:48
    内容：《Programming Rust 2nd Edition》第541-543页。
        Rust程序中，通过引入std::future::Future trait来实现对异步操作的支持。

        相对于同步运行的函数，异步函数的返回类型使用Futureh进行包裹。 如下代码中返回的即是：未来会返回的类型为Result<usize>的值（个人理解）。。。。。
        ```
        fn read_to_string(&mut self, buf: &mut String) -> impl Future<Output = Result<usize>>;
        ```

## 第 141 个番茄时间

    时间：2022.04.04 17:48
    内容：《Programming Rust 2nd Edition》第543-545页。
        | 由于某些计算（或者网络请求）尚未结束，我们需要一个对象来代理这个未知的结果，于是就有了这些构造（future、promise等）。术语“future”、“promise”、“delay”和“deferred”通常可以互换使用。

        调用异步函数时不会实际执行，而是在轮询(poll)时才具体执行？？？？？   anyway，必须要考虑参数的生命周期。正确的函数签名如下：
        ```
        fn read_to_string<'a>(&'a mut self, buf: &'a mut String) -> impl Future<Output = Result<usize>> + 'a;
        ```

        async-std crate提供了所有std::io的异步版本，包括带有read_to_string方法的异步Read trait。

        [Async Functions and Await Expressions]

## 第 142 个番茄时间

    时间：2022.04.04 19:08
    内容：《Programming Rust 2nd Edition》第545-547页。
        调用异步函数时返回的future中包含所有需要的参数和本地变量等信息。
        第一次轮询future时，正式执行代码。

        .await 表达式：获取future的所有权并进行轮询(poll)操作，返回最终值或者Poll::Pending。

        Rust尚不允许trait中包含异步方法。 自由函数或属于某类型的函数能够异步。

        如果确实需要在trait中包含异步函数，可以考虑使用：async-trait crate。（采用了基于宏的变通办法）。。。

        [Calling Async Functions from Synchronous Code: block_on]
        在同步代码中可以通过 async_std::task::block_on 函数来调用异步函数。
        block_on 函数本身是一个最终能获取内部异步函数执行结果的同步函数（阻塞函数）。 可以理解为是一个适配器: async func ---> sync func。

        所以，不能在异步代码中使用block_on函数。

## 第 143 个番茄时间

    时间：2022.04.04 23:03
    内容：《Programming Rust 2nd Edition》第547-550页。
        同步代码中调用异步函数： block_on (async_std::task::block_on)
        异步代码中调用异步函数： await 
        ？？？

## 第 144 个番茄时间

    时间：2022.04.05 16:36
    内容：《Programming Rust 2nd Edition》第550-553页。
        [Spawning Async Tasks]
        async_std::task::spawn_local 对应 std::thread::spawn ？？？

        如果要使用 spawn_local，需要引用 async-std 的 unstable 特性。

        std::thread::spawn(c)               c = closure
        async_std::task::spawn_local(f)     f = future

        spawn_local返回的future通过await触发执行？？？？  block_on调用？？？

## 第 145 个番茄时间

    时间：2022.04.05 17:23
    内容：《Programming Rust 2nd Edition》第553-555页。
        在异步任务中不宜放入需要长时间运行的计算，避免造成实际的阻塞。一般考虑放入新的线程中，，，

        如确有需要在异步任务中放入长时间计算任务，使用：yield_now 和 spawn_blocking。

        [Async Blocks]  异步块
        异步块返回最后一个表达式的future值，可以在块中使用.await表达式。

        在异步块中使用?操作符（或 return 表达式），只是从块内返回，而非整个函数。
        
        如果涉及到变量的移动，使用： async move { ... }

## 第 146 个番茄时间

    时间：2022.04.05 18:38
    内容：《Programming Rust 2nd Edition》第555-557页。
        异步块提供了一种简洁的方式来分离异步运行的代码部分？？？  减少对参数生命周期的考虑。

        ```
        let future = async { 
            ...
            input.read_line(&mut line).await?;
            ...
            Ok::<(), std::io::Error>(())   // 指定异步块可能返回的错误类型。
        };
        ```
        
        [Building Async Functions from Async Blocks]    通过异步块构建异步函数。
        ？？？

## 第 147 个番茄时间

    时间：2022.04.05 19:35
    内容：《Programming Rust 2nd Edition》第557-560页。
        [Spawning Async Tasks on a Thread Pool]     在线程池中运行异步任务。
        async_std::task::spawn  用法类似于 async_std::task::spawn_local。
        与spawn_local不同的是，对于spawn返回的future在线程池有空闲时就会开始运行，而非必需调用block_on方法。 某一个异步任务可能在不同的线程执行。。。。

        实践中，spawn 比 spawn_local使用广泛。

        thread-local    存储
        task- local     存储

        [But Does Your Future Implement Send?]
        spawn有一个限制：必须实现Send trait。    （因为使用了线程池）
        
        `async_std::task::spawn`的签名如下：
        ```
        pub fn spawn<F, T>(future: F) -> JoinHandle<T>
        where
            F: Future<Output = T> + Send + 'static,
            T: Send + 'static, 
        ```

        解决办法：
            1. 未实现Send trait的值的生命周期不覆盖await表达式。 从而该值不会保存到future中。
            2. 使用实现了Send trait的变量值。  比如： Rc<String> 替换为 Arc<String>。

## 第 148 个番茄时间

    时间：2022.04.05 20:12
    内容：《Programming Rust 2nd Edition》第560-562页。
        如果不能保证future实现了Send trait，只能在当前线程中使用spawn_local。

        [Long Running Computations: yield_now and spawn_blocking]
        async_std::task::yield_now      异步代码中主动yield。
        调用方式： async_std::task::yield_now().await;

        async_std::task::spawn_blocking 把函数过程扔到独立线程处理，当前异步任务Pending。  
        即：某异步任务特别耗时间，所以将具体任务打包派发到额外的线程，当前的异步任务对其做监控。  
        不赚差价老中间商！！！

## 第 149 个番茄时间

    时间：2022.04.06 22:17
    内容：《Programming Rust 2nd Edition》第562-564页。
        [Comparing Asynchronous Designs]
        Rust calls them “futures,”
        JavaScript calls them “promises,”
        C# calls them “tasks,” 

        异步调用什么都不做，直到您将其传递给block_on、spawn或spawn_local等函数，该函数将轮询它并推动工作完成。

        在rust中，当future传递到executors(block_on, spawn, or spawn_local)后才开始具体执行直到任务完成。

        [A Real Asynchronous HTTP Client]
        ```
        pub async fn many_requests(urls: &[String]) -> Vec<Result<String, surf::Exception>> {
            let client = surf::Client::new();
            let mut handles = vec![];
            for url in urls {
                let request = client.get(&url).recv_string();
                handles.push(async_std::task::spawn(request));
            }
            let mut results = vec![];
            for handle in handles {
                results.push(handle.await);
            }
            results
        }
        fn main() {
            let requests = &[
                "http://example.com".to_string(),
                "https://www.red-bean.com".to_string(),
                "https://en.wikipedia.org/wiki/Main_Page".to_string(),
            ];
            let results = async_std::task::block_on(many_requests(requests));
            for result in results {
                match result {
                    Ok(response) => println!("*** {}\n", response),
                    Err(err) => eprintln!("error: {}\n", err),
                }
            }
        }

        ```

## 第 150 个番茄时间

    时间：2022.04.07 00:18
    内容：《Programming Rust 2nd Edition》第564-568页。
        [Chapter 20.2 -- An Asynchronous Client and Server] async-chat 项目示例

        ```
        cargo new --lib async-chat

        async-chat
            ├── Cargo.toml
            └── src
                ├── lib.rs
                ├── utils.rs
                └── bin
                    ├── client.rs
                    └── server
                        ├── main.rs
                        ├── connection.rs
                        ├── group.rs
                        └── group_table.rs

        $ cargo run --release --bin server -- localhost:8088
        $ cargo run --release --bin client -- localhost:8088
        ```

        [Error and Result Types]
        ```
        use std::error::Error;

        pub type ChatError = Box<dyn Error + Send + Sync + 'static>;
        pub type ChatResult<T> = Result<T, ChatError>;
        ```
        各类Error通过?操作符均可自动转换为ChatError。

        在真实项目中，建议使用 anyhow crate。  

## 第 151 个番茄时间

    时间：2022.04.07 22:49
    内容：《Programming Rust 2nd Edition》第568-571页。
        [[Taking User Input: Asynchronous Streams]]
        async_std::stream 模块相当于是模拟iterator的异步实现。可以理解为Iterator和Future traits的混合体。（缝合怪？？？ LOL）

        如同iterator一样，Stream具有关联项目类型以及标识序列返回的Option值。 也如同future一样，Stream需要通过轮询来获取next值。（poll_next ？？？） 

        所以，stream = 类迭代器的future ？？？？

        由于Stream的很多实用方法定义在StreamExt中，所以实际使用时，必须引入`async_std::prelude::*`。 即： use async_std::prelude::*; 

        [[Sending Packets]]

        serde_json可以直接序列化输出到stream，但只支持同步的streams。

        ？？？  好像还是不清楚 serde 与 serde_json 的区别是什么？？？？ 

## 第 152 个番茄时间

    时间：2022.04.08 22:22
    内容：《Programming Rust 2nd Edition》第571-574页。
        [[Receiving Packets: More Asynchronous Streams]]
        DeserializeOwned 是Deserialize更严格的变体？？？ 声明周期比buffer更长？？？

        [[The Client’s Main Function]]
        async_std::prelude::FutureExt::race 同时等待多个future，返回第一个完成的。


## 第 153 个番茄时间

    时间：2022.04.08 23:46
    内容：《Programming Rust 2nd Edition》第574-579页。
        [[The Server’s Main Function]]

        [[Handling Chat Connections: Async Mutexes]]
        略微难了点儿，跑马观花。。。。。。。。。
        async_std::sync::Mutex 可以跨线程~~~~

        [[The Group Table: Synchronous Mutexes]]
        

## 第 154 个番茄时间

    时间：2022.04.10 01:44
    内容：《Programming Rust 2nd Edition》第579-583页。
        [[Chat Groups: tokio’s Broadcast Channels]]

        [Primitive Futures and Executors: When Is a Future Worth Polling Again?]
        轮询future时，如果返回Poll::Pending，则在future中保存waker，当值得再次轮询是，executor就调用相应的waker。

## 第 155 个番茄时间

    时间：2022.04.11 23:29
    内容：《Programming Rust 2nd Edition》第584-585页。
        [[Invoking Wakers: spawn_blocking]]
        spawn_blocking: 在另一个线程上运行闭包，并返回其future。 

## 第 156 个番茄时间

    时间：2022.04.12 01:34
    内容：《Programming Rust 2nd Edition》第585-588页。
        [[Implementing block_on]]
        太南了，，，，，，，，，，，，，

        先配置为阻塞，然后再闭包解阻塞？？？？

        pin!(future)  ???
        获取future的所有权并声明类型为Pin<&mut F>的同名新变量并借用？？？？   （轮询函数需要~~~）
        原因： 异步函数和异步块的future必须通过Pin引用，然后才能轮询。~????

## 第 157 个番茄时间

    时间：2022.04.12 19:25
    内容：《Programming Rust 2nd Edition》第588-588页。
        [Pinning]   锚定？ 固定？ 钉住？RFC2349
        为何异步函数的future不能任意handle处理？
        Pin 如何保障 future的安全？
        使用Pin????

        https://zhuanlan.zhihu.com/p/348648305

        https://folyd.com/blog/rust-pin-unpin/    ☆☆☆
        
        Pin自身是一个智能指针。为什么呢？因为他impl了Deref和DerefMut。
        Pin包裹的内容只能是指针，不能是其他普通类型。比如Pin<u32>就没有意义。
        Pin具有“钉住”T不能移动的功能，这个功能是否生效取决于T是否impl Unpin。简单的说，如果T实现了Unpin，Pin的“钉住”功能完全失效了，这时候的Pin<P<T>>就等价于P<T>。
        Unpin是一个auto trait，编译器默认会给所有类型实现Unpin。唯独有几个例外，他们实现的是!Unpin。这几个例外是PhantomPinned，编译器为async/await desugar之后生成的impl Future的结构体。
        所以Pin<P<T>>默认情况下的“钉住”功能是不生效的，只针对上面说的这几个impl !Unpin的情况生效。

        2018年官方异步组引入Pin API的初衷就是为了解决Future内部自引用的问题。因为async/await就是通过Generator实现的，Generator是通过匿名结构体实现的。如果async函数中存在跨await的引用，会导致底层Generator存在跨yield的引用，那根据Generator生成的匿名结构体就会是一个自引用结构体！然后这个自引用结构体会impl Future，异步的Runtime在调用Future::poll()函数查询状态的时候，需要一个可变借用（即&mut Self）。如果这个&mut Self不包裹在Pin里面的话，开发者自己impl Future就会利用std::mem::swap()之类的函数move掉&mut Self！所以这就是Future的poll()必须要使用Pin<&mut Self>的原因。

        ----------------------------
        
        关于async/await的原理，强烈推荐阅读这两本书：

            https://rust-lang.github.io/async-book
            https://cfsamson.github.io/books-futures-explained


## 第 158 个番茄时间

    时间：2022.04.12 21:52
    内容：《Programming Rust 2nd Edition》第588-592页。
        [[The Two Life Stages of a Future]]
        poll方法要求future以Pin<&mut Self>形式作为参数值。 Pin智慧指针禁止数据move。

## 第 159 个番茄时间

    时间：2022.04.12 22:59
    内容：《Programming Rust 2nd Edition》第592-595页。
        [[Pinned Pointers]]
        Pin<&mut T> , Pin<Box<T>>

        构建方法：
            - pin!宏。
            - Box::pin
            - Pin::from(boxed)

        所有Pin<pointer to T>类型都可以通过as_mut方法来解引用以返回poll需要的Pin<&mut T>。

        执行器(block_on, spawn等)在内部自动实现了再引用。。。

        [[The Unpin Trait]]
        ...

## 第 160 个番茄时间

    时间：2022.04.13 01:31
    内容：《Programming Rust 2nd Edition》第595-600页。
        [When Is Asynchronous Code Helpful?]
        相对于多线程，使用更小的内存使用。
        相对于多线程，创建异步任务更快。
        相对于多线程，任务切换速度更快。

        [CHAPTER 21 -- Macros]

## 第 161 个番茄时间

    时间：2022.04.14 00:02
    内容：《Programming Rust 2nd Edition》第600-603页。  
        [Macro Basics]
        macro_rules! 是rust中定义宏的主要方法。  感叹号"!"在定义时不需要，在调用时需要。

        file!, line!, macro_rules! 是内建在编译器中的宏。

        宏调用时可使用圆括号、方括号、花括号：
        ```
            assert_eq!(gcd(6, 10), 2);
            assert_eq![gcd(6, 10), 2];
            assert_eq!{gcd(6, 10), 2}           // 花括号后可以不写分号。
        ```
        按照惯例，调用 assert_eq! 时使用圆括号，vec! 使用方括号，macro_rules! 使用花括号。

        [[Basics of Macro Expansion]]
        宏必须先定义，然后才能使用。

## 第 162 个番茄时间

    时间：2022.04.14 01:08
    内容：《Programming Rust 2nd Edition》第603-607页。  
        [[Unintended Consequences]]
            - 用中间变量存储值。
            - 使用值的引用来进行比较，而非数据本身。

        [[Repetition]]
        ```
        macro_rules! vec {
            ($elem:expr ; $n:expr) => {
                        ::std::vec::from_elem($elem, $n)
                    };
            ($($x:expr),*)=>{ <[_]>::into_vec(Box::new([ $( $x ),* ]))
            }; ($($x:expr),+,)=>{
                        vec![ $( $x ),* ]
                    };
            }
        ```

        // <[_]>::into_vec(Box::new([ $( $x ),* ]))   这个的具体实现未知。。。。。。

## 第 163 个番茄时间

    时间：2022.04.15 00:45
    内容：《Programming Rust 2nd Edition》第607-611页。  
        [Built-In Macros]
        file!(), line!(), column!()

        stringify!(...tokens...)

        concat!(str0, str1, ...)

        cfg!(...)           条件编译
        ```
        #[cfg(target_os = "linux")]
        fn are_you_on_linux() {
            println!("You are running linux!")
        }

        -------------------

        if cfg!(target_os = "linux") {
            println!("Yes. It's definitely linux!");
        }
        ```
        env!("VAR_NAME")        获取环境变量

        option_env!("VAR_NAME")

        include!("file.rs")

        include_str!("file.txt")

        include_bytes!("file.dat")

        todo!(), unimplemented!()

        matches!(value, pattern)

        [Debugging Macros]
        cargo build --verbose 显示具体的rustc命令行，然后给命令行追加 -Z unstable-options --pretty ???

        log_syntax!() 

        #![feature(trace_macros)]
            trace_macros!(true);
            ...一些宏...
            trace_macros!(false);

        [Building the json! Macro]
        
        --------------
        Rust宏小册： https://zjp-cn.github.io/tlborm/

## 第 164 个番茄时间

    时间：2022.04.16 01:00
    内容：《Programming Rust 2nd Edition》第611-614页。  
        [[Fragment Types]]
        Table 21-2. Fragment types supported by macro_rules!
        - expr
        - stmt      难用
        - ty       ???  还是 try ? 文档勘误？
        - path
        - pat
        - item
        - block
        - meta
        - ident
        - literal
        - lifetime
        - vis
        - tt        token tree

        ```
        macro_rules! json {
            (null) => {
                Json::Null
            };
            ([ $( $element:tt ),* ]) => { Json::Array(...)
            };
            ({ $( $key:tt : $value:tt ),* }) => {
                        Json::Object(...)
                    };
            ($other:tt) => {
            ... // TODO: Return Number, String, or Boolean
            }; 
        }
        ```

## 第 165 个番茄时间

    时间：2022.04.16 17:36
    内容：《Programming Rust 2nd Edition》第614-618页。  
        [[Recursion in Macros]]
        ```
        macro_rules! json {
            (null) => {
                Json::Null
            };
            ([ $( $element:tt ),* ]) => { Json::Array(vec![ $( json!($element) ),* ])
            };
            ({ $( $key:tt : $value:tt ),* }) => {
                        Json::Object(Box::new(vec![
                            $( ($key.to_string(), json!($value)) ),*
                        ].into_iter().collect()))
                    };
            ( $other:tt ) => {
            Json::from($other) // Handle Boolean/number/string
            }; 
        }
        ```

        [[Scoping and Hygiene]]

## 第 166 个番茄时间

    时间：2022.04.16 19:12
    内容：《Programming Rust 2nd Edition》第618-622页。
        。。。。。

        [[Importing and Exporting Macros]]
        使用 #[macro_use] 属性 暴露宏到父模块。

         #[macro_export]   暴露到其他模块？？？

## 第 167 个番茄时间

    时间：2022.04.16 20:16
    内容：《Programming Rust 2nd Edition》第622-624页。
        [Avoiding Syntax Errors During Matching]
        - 避免混淆规则。  比如使用不同的indentifier。
        - 将更具体的规则前置。  

        [Beyond macro_rules!]
        procedural macro   

        Yes!  I hate macros。

## 第 168 个番茄时间

    时间：2022.04.16 23:45
    内容：《Programming Rust 2nd Edition》第625-626页。
        [CHAPTER 22 -- Unsafe Code]
        unsafe code 可以获得调用标注库中的unsafe函数、解引用不安全指针、低啊用其他语言函数等能力。

        rust的常规安全检查仍旧有效：类型检查、生命周期检查、对索引的边界检查等。。。    

        [Unsafe from What?]
        太难看懂了，，，，

## 第 169 个番茄时间

    时间：2022.04.17 13:20
    内容：《Programming Rust 2nd Edition》第626-631页。
        [Unsafe Blocks]
        unsafe块解锁4项能力：
            - 调用unsafe函数。
            - 解引用原始指针。
            - 访问union体字段？？？
            - 访问可修改static变量。
            - 访问由外来函数接口声明的函数和变量。

        unsafe块的意义：
            - 不会意外使用unsafe特性。
            - 代码评审人会格外关注unsafe块。
            - 慎重使用。

        [Example: An Efficient ASCII String Type]

## 第 170 个番茄时间

    时间：2022.04.17 15:32
    内容：《Programming Rust 2nd Edition》第631-634页。
        [Unsafe Block or Unsafe Function?]
        一般优先考量使用Unsafe函数，而非Unsafe块。

        函数是否安全与函数体内部是否使用unsafe函数或块无关。 真正决定函数安全与否的是有无协议(约定？)~~~

        如果倾向于让人查看unsafe细节的时候，使用Unsafe块？？？？？

## 第 171 个番茄时间

    时间：2022.04.17 18:01
    内容：《Programming Rust 2nd Edition》第634-636页。 实阅中文第一版。
        [Undefined Behavior]
        Rust认为不会在相关代码中出现的行为。
        
        程序行为良好的Rust规则：
        • The program must not read uninitialized memory.
        • The program must not create invalid primitive values:
            — References, boxes, or fn pointers that are null
            — bool values that are not either a 0 or 1
            — enum values with invalid discriminant values
            — char values that are not valid, nonsurrogate Unicode code points
            — str values that are not well-formed UTF-8
            — Fat pointers with invalid vtables/slice lengths
            — Any value of the type !
        • The rules for references explained in Chapter 5 must be followed. No reference may outlive its referent; shared access is read-only access; and mutable access is exclusive access.
        • The program must not dereference null, incorrectly aligned, or dangling pointers.
        • The program must not use a pointer to access memory outside the allocation with which the pointer is associated. We will explain this rule in detail in “Deref‐ erencing Raw Pointers Safely” on page 641.
        • The program must be free of data races. A data race occurs when two threads access the same memory location without synchronization, and at least one of the accesses is a write.
        • The program must not unwind across a call made from another language, via the foreign function interface, as explained in “Unwinding” on page 158.
        • The program must comply with the contracts of standard library functions.

## 第 172 个番茄时间

    时间：2022.04.17 22:07
    内容：《Programming Rust 2nd Edition》第636-638页。实阅中文第一版。
        Unsafe Traits（不安全特型）：某些特征在使用时必须满足一些rust无法自动检查或强制的协议(contract)。

        通常，变量类型与不安全特型绑定的函数本身也使用不安全特性。 该函数的协议依赖于不安全特型的协议。

        不安全特型的经典例子是： std::marker::Send 和 std::mark::Sync。
            - Send 要求实现者安全地移动到另一个线程，
            - Sync 要求实现者安全地通过共享引用在线程之间共享。
        如果给一个不满足条件/协议的类型实现Send，可能会导致如std::sync::Mutex不再安全，从而无法避免数据挣用。

        标准库中有一个不安全特型：  core::nonzero::Zeroable，将类型所有字节设置为0来初始化。
        ```
        pub unsafe trait Zeroable {}

        unsafe impl Zeroable for u8 {}
        unsafe impl Zeroable for i32 {} 
        unsafe impl Zeroable for usize {}
        // and so on for all the integer types
        ```

        ```
        use core::nonzero::Zeroable;

        fn zeroed_vector<T>(len: usize) -> Vec<T> 
            where T: Zeroable
        {
            let mut vec = Vec::with_capacity(len); 
            unsafe {
                        std::ptr::write_bytes(vec.as_mut_ptr(), 0, len);
                        vec.set_len(len);
                    }
            vec
        }
        ```

## 第 173 个番茄时间

    时间：2022.04.18 01:21
    内容：《Programming Rust 2nd Edition》第638-641页。 实阅中文第一版。
        [Raw Pointers]  原始指针，不受约束的指针。 等同于C、C++中的指针。

        可以用原始指针来构建任意结构体，比如双向链表或任意对象图。 只能在unsafe块中进行解引用。

        两种原始指针：
            - *mut T        允许修改其引用目标
            - *const T      只允许读取其引用目标
        PS： 没有 *T 类型的原始指针，即必须指定 const 或者 mut。

        可以把引用转换为原始指针，然后使用 * 操作符对其进行解引用。

        对原始指针的创建、传递、比较都是安全的(safe)，只有解引用才是非安全的(unsafe)。

        指向非固定大小类型(Unsized)的原始指针是胖指针。

        原始指针的解引用必须是**显式的**:   (*raw).filed 或 (*raw).method(...)
            - . 操作符不会隐式解引用原始指针。 
            - 原始指针没有实现Deref。
            - 比较操作符(如：== > 等)比较的是原始指针的地址，而非指向的值。 
            - std::fmt::Display 等格式化trait自动跟随引用？？？ 但不会处理原始指针？？？

        Rust的as操作符可以将普通引用转换为原始指针，或者将原始指针转化为另一种原始指针（可能需要多步骤完成）。
        ```
        &vec![42_u8] as *const String; // error: invalid conversion 
        &vec![42_u8] as *const Vec<u8> as *const String; // permitted
        ```
        原始指针不能转换为引用，比如在unsafe块中对原始指针解引用，然后再借用得到的值。但需要特别小心：因为这种方式产生的引用具有不受限的生命周期。

        不同于引用，原始指针既不是Send，也不是Sync。因此，任何包含原始指针的类型都没有实现Send和Sync特型。 so what？？？？  M。。。 F。。。。
        
        ------------
        Send 和 Sync的实现？？？  忘记了。。。。。

## 第 174 个番茄时间

    时间：2022.04.19 02:00
    内容：《Programming Rust 2nd Edition》第641-643页。 实阅中文第一版。
        [[Dereferencing Raw Pointers Safely]]
        安全使用原始指针的常识性指南：
            - 解引用空指针或悬空指针是未定义行为。
            - 解引用没有与他们引用目标类型正确对齐的指针是未定义行为。
            - 如果想从解引用后的原始指针中借用值，必须遵循“引用安全规则”。。。。（引用的生命周期不应该比其引用的目标还长；共享引用是只读的；可修改的引用是专有访问）。
            - 只有当原始指针是其类型的良好值时，您才能使用它的引用。 （对应于上述第二个点吧？？？？）
            - 如果想在原始指针上使用offset或wrapping_offset方法，必须保证指针只指向变量或原本指针所指向的堆内存块中的字节？？？？？？？ 
            - 如果要给原始指针的引用目标赋值，必要遵循引用目标所在类型的不变性。

        不违反类型不变性？？？？

        [Example: RefWithFlag]
        std::marker::PhantomData    是什么鬼，貌似忘记了已经。。。

## 第 175 个番茄时间

    时间：2022.04.21 01:43
    内容：《Programming Rust 2nd Edition》第643-644页。 实阅中文第一版。
        任何包含引用的结构体必须不能“活”得比它们借用的值更久，以避免引用变成悬空指针。
        在结构体中，包含一个类型为 PhantomData<&'a T> 的字段，纯粹只用于约束生命周期。

        生命周期，，，，，，，，

        [[Nullable Pointers]]   可空指针
        std::ptr::null<T>           *const T 空指针
        std::ptr::null_mut<T>       *mut T 空指针

        通过is_null(), as_ref(), as_mut() 来判断是否为空指针。  ？？？？

        so，可空指针干啥用的？

## 第 176 个番茄时间

    时间：2022.04.21 23:14
    内容：《Programming Rust 2nd Edition》第645-647页。 实阅中文第一版。
        [[Type Sizes and Alignments]]
        std::mem::size_of::<T>()    返回类型T的长度
        std::mem::align_of::<T>()   返回类型T要求的对齐值。
        ```
        assert_eq!(std::mem::size_of::<i64>(), 8);
        assert_eq!(std::mem::align_of::<(i32, i32)>(), 4);
        ```
        std::mem::size_of_val 和 std::mem::align_of_val 分别返回值的大小和分配量？？？ 可用于Sized和Unsized类型的引用。

        [[Pointer Arithmetic]]  指针算术
        ptr.offset(i)

        ptr.wrapping_offset(i)

## 第 177 个番茄时间

    时间：2022.04.23 01:15
    内容：《Programming Rust 2nd Edition》第647-650页。 实阅中文第一版。
        [[Moving into and out of Memory]]
        初始化值真正的定义是将其视作为存活值。？？？

        Rust跟踪在编译时存活的本地变量，并阻止你使用其值已移动到其他地方的变量。Vec、HashMap、Box等类型能动态跟踪其缓冲区。如果您实现一种管理自己内存的类型，则也需要这样做。

        std::ptr::read(src)             src应该是一个 *const T 原始指针。 Vec::pop() 
        std::ptr::write(dest, value)    dest应该是一个 *mut T 原始指针。    Vec::push()

        std::ptr::copy(src, dst, count)
        ptr.copy_to(dst, count)
        std::ptr::copy_nonoverlapping(src, dst, count)  相比于copy，要求源、目标内存块不能重叠。

        read_unaligned, write_unaligned     类似于read 和 write，但不要求指针对齐~~·
        read_volatile, write_volatile       相当于C或C++中的volatile(易失性)读写。???

## 第 178 个番茄时间

    时间：2022.04.25 00:03
    内容：《Programming Rust 2nd Edition》第651-654页。 实阅中文第一版。
        [Example: GapBuffer]
        用于文本编辑器中，，，， 以便于高效插入、删除。。。。

## 第 179 个番茄时间

    时间：2022.04.26 00:02
    内容：《Programming Rust 2nd Edition》第654-657页。 实阅中文第一版。
        核心思路就是: 光标为止就是gap的位置，插入或删除都不会引起大量数据位移，只有在移动光标时因为gap的移动才会移动数据。

        虽然set_position必须使用copy在间隙中来回移动元素，而 enlarge_gap可以使用copy_nonoverlapping，因为它正在将元素移动到一个全新的缓冲区。

## 第 180 个番茄时间

    时间：2022.04.26 21:03
    内容：《Programming Rust 2nd Edition》第657-659页。
        [[Panic Safety in Unsafe Code]]
        说人话：在不安全代码中，需要考虑panic情况。。。。   I guess。

        [Reinterpreting Memory with Unions]   重新解读Union的内存？？？

        ```
        let mut one = FloatOrInt { i: 1 }; 
        assert_eq!(unsafe { one.i }, 0x00_00_00_01); 
        one.f = 1.0;
        assert_eq!(unsafe { one.i }, 0x3F_80_00_00);
        ```

        不同于enum，union没有tag ？？？  所以读取union的字段总是不安全的。

## 第 181 个番茄时间

    时间：2022.04.26 23:00
    内容：《Programming Rust 2nd Edition》第660-663页。
         #[repr(C)] 保证所有字段从偏移量0的位置开始存储，，，
        可以利用Union来提取数据中的某个byte。
        ```
        #[repr(C)]
        union SignExtractor { 
            value: i64,
            bytes: [u8; 8] 
        }

        fn sign(int: i64) -> bool {
            let se = SignExtractor { value: int};
            println!( "{:b} ({:?})", unsafe { se.value }, unsafe { se.bytes }); 
            unsafe { se.bytes[7] >= 0b10000000 }
        }

        assert_eq!(sign(-1), true); 
        assert_eq!(sign(1), false); 
        assert_eq!(sign(i64::MAX), false); 
        assert_eq!(sign(i64::MIN), true);
        ```

        [Matching Unions]
        必须匹配具体的字段值。
        ```
        unsafe {
            match u {
                SmallOrLarge { s: true } => { println!("boolean true"); } 
                SmallOrLarge { l: 2 } => { println!("integer 2"); }
                _ => { println!("something else"); }
            }
        }
        ```

        [Borrowing Unions]

        [CHAPTER 23 -- Foreign Functions Interface]   FFI

## 第 182 个番茄时间

    时间：2022.04.27 13:32
    内容：《Programming Rust 2nd Edition》第664-666页。
        [Finding Common Data Representations]
        Rust的bool类型等同于C/C++的bool。
        C/C++中的指针对应于Rust中的原始指针( *mut T , *const T)。
        
        要定义与C结构兼容的Rust结构类型，您可以使用#[repr(C)]属性。
        #[repr(C)]      按C语言的风格编译？？？？？   repr == representation
        ```
        use std::os::raw::{c_char, c_int};

        #[repr(C)]
        pub struct git_error {
            pub message: *const c_char,
            pub klass: c_int
        }
        ```

## 第 183 个番茄时间

    时间：2022.04.27 23:00
    内容：《Programming Rust 2nd Edition》第667-669页。
        与String和str相比，CString和CStr的方法非常有限，仅限于构建和转换为其他类型。

        [Declaring Foreign Functions and Variables]
        使用 extern 块来声明来之其他库的函数和变量。
        ```
        use std::os::raw::c_char;
        extern {
            fn strlen(s: *const c_char) -> usize;
        }
        // ------------------------
        use std::ffi::CString;
        let rust_str = "I'll be back";
        let null_terminated = CString::new(rust_str).unwrap();
        unsafe {
            assert_eq!(strlen(null_terminated.as_ptr()), 12);
        }
        ```

        还可以在 extern块中定义全局变量。 POSIX系统有一个叫environ的全局变量，保存在进程的环境变量。

        ```
        // C中
        extern char **environ;
    
        // Rust中
        use std::ffi::CStr;
        use std::os::raw::c_char;
        extern {
            static environ: *mut *mut c_char;
        }

        // --------------------
        unsafe {
            if !environ.is_null() && !(*environ).is_null() {
                let var = CStr::from_ptr(*environ);
                println!("first environment variable: {}",ar.to_string_lossy())
            }
        }
        ```

## 第 184 个番茄时间

    时间：2022.04.28 00:01
    内容：《Programming Rust 2nd Edition》第669-674页。
        [Using Functions from Libraries]
        使用外部库的函数，需要在extern代码块前置 #[link] 属性。
        ```
        use std::os::raw::c_int;
        #[link(name = "git2")] 
        extern {
            pub fn git_libgit2_init() -> c_int;
            pub fn git_libgit2_shutdown() -> c_int; 
        }
        fn main() { 
            unsafe {
                git_libgit2_init();
                git_libgit2_shutdown();
            }
        }
        ```
        需要写构建脚本：build.rs。
        还需要设置LD路径？  LD_LIBRARY_PATH (Linux), DYLD_LIBRARY_PATH (macOS), PATH (Windows)。

        还可以将外部库静态链接到rust包中。
        Cargo约定提供访问C库的crate必须命名为 LIB-sys 格式。（LIB 为 C库的名字）

        [A Raw Interface to libgit2]

## 第 185 个番茄时间

    时间：2022.04.28 11:33
    内容：《Programming Rust 2nd Edition》第675-678页。
        ```
        extern int git_repository_open(git_repository **out, const char *path);
        // ---------------------
        pub fn git_repository_open(out: *mut *mut git_repository, path: *const c_char) -> c_int;
        ```

        bindgen crate 可以根据C库header自动生成对应的rust声明。

        有点复杂。。。。

## 第 186 个番茄时间

    时间：2022.04.28 18:36
    内容：《Programming Rust 2nd Edition》第678-682页。
        
        MaybeUninit<T> 用于为变量预留内存（但非初始化）。
        as_mut_ptr() 返回一个可修改的原始指针；
        assume_init() 直接将原始指针标记为初始化了的指针？？？？

        [A Safe Interface to libgit2]

## 第 187 个番茄时间

    时间：2022.04.28 20:52
    内容：《Programming Rust 2nd Edition》第682-685页。 
        std::sync::Once 类型帮助初始化代码线程安全的运行。 只有第一个调用 ONCE.call_once() 的线程会得到提供的闭包。

## 第 188 个番茄时间

    时间：2022.04.28 23:18
    内容：《Programming Rust 2nd Edition》第685-690页。 

        过了一遍，实际用时，还需要细细琢磨。。。。

        本书结束，接来下实际开始做这个项目了。。。。。。



----------------------------------------------

## 第 189 个番茄时间
    时间：2022.04.29 12:42
    内容：需求分析 - 思维导图。

    - 用户相关
        - 用户注册
        - 用户登录
        - 用户注销
    - Dashboard
    - 目标任务
        - 任务新建
            目标描述，消极记录次数设定，积极记录，其它的任务放弃条件。
        - 子任务？
        - 任务里程碑记录
    - 消极记录
        - 记录、查询
    - 积极记录
        - 记录、查询

## 第 190 个番茄时间
    时间：2022.04.29 23:59
    内容：纠结接下来该做什么，怎么做，，，，
        本来想做一个《axum解读》，但回过头来想，好像走偏了，，，， 大概率做不好，还费时间分心了主要目标。。。。
        so，搞清楚axum怎么用就好了！！！！ 

## 第 191 个番茄时间
    时间：2022.04.30 01:14
    内容：docs.rs/axum
        - Routing (路由)
        - Handlers (处理程序)
            handler 是一个接收 extractor 作为参数异步函数，其返回值可转换为response。
        - Extracotrs (提取器)
            extractor 是一种实现了 FromRequest 的类型，用于从请求中提取handler需要的数据。

## 第 192 个番茄时间
    时间：2022.04.30 13:52
    内容：
    - Responses (响应)
        能从handler返回的实现了 `IntoResponse` 的类型？
    - Error handling (错误处理)
        axum 旨在拥有一个简单且可预测的错误处理模型。 这意味着将错误转换为响应很简单，并且可以保证所有错误都得到处理。 
    - Middleware (中间件)
        axum的中间件本质就是一个包含了tower Service的结构体？ 可以灵活的串联在处理过程的任何位置~？？
        session，权限、jwt、数据库连接池都可以通过中间件提供给handler？？？？
    
## 第 193 个番茄时间
    时间：2022.04.30 15:27
    内容：docs.rs/axum
        - Sharing State With Handlers (handler间状态共享？)
            在处理程序之间共享某些状态是很常见的，例如共享数据库连接池或与其他服务的客户端。
            两种最常见的方法是：
            - 使用请求扩展
                从handler中提取状态最简单的方法是使用 `Extension` 作为layer和extractor。
                这种方法的缺点是，如果尝试提取的扩展不存在，将收到运行时错误（特别是 `500 Internal Server Error` 响应），可能是因为忘记添加中间件或提取错误的类型。

            - 使用闭包捕获
                状态也可以使用闭包捕获直接传递给处理程序。
                这种方法的缺点是，它比使用扩展更冗长。
                - [ ]  示例学习：使用闭包捕获方式进行handler间状态共享

        - Building Integrations For Axum (为axum构建集成)
            在自建库时，如果需要实现 FromRequest 或 IntoResponse ，最好依赖 axum-core crate，而非axum。 可以保持核心类型和特型，但不太可能有重大改变。

## 第 194 个番茄时间
    时间：2022.04.30 20:52
    内容：https://docs.rs/axum/latest/axum/struct.Router.html


## 第 195 个番茄时间
    时间：2022.04.30 23:03
    内容：https://docs.rs/axum/latest/axum/handler/index.html


## 第 196 个番茄时间
    时间：2022.05.01 00:27
    内容：https://docs.rs/axum/latest/axum/extract/index.html
        看了一半，Next：Accessing inner errors


## 第 197 个番茄时间
    时间：2022.05.01 01:35
    内容：https://docs.rs/axum/latest/axum/extract/index.html
        粗略过了一遍，很多懵逼之处。。。

## 第 198 个番茄时间
    时间：2022.05.01 11:00
    内容：
        unimplemented! vs todo!
            - unimplemented!()    带有特定信息的panic!()。  用于指示相关的实现代码并不应该被用到，如果用到了就是错误的，抛出panic ？？？？
            - todo!()             带有特定信息的panic!()。  指示相关代码尚未实现（以后会实现~）

        https://docs.rs/axum/latest/axum/response/index.html
        任何实现 IntoResponse 的类型都可以作为handler的返回值。 axum 提供了常见类型的实现。

## 第 199 个番茄时间
    时间：2022.05.01 
    内容：https://docs.rs/axum/latest/axum/error_handling/index.html
        axum::error_handling::HandleError
        axum::error_handling::HandleErrorLayer

## 第 200 个番茄时间
    时间：2022.05.01 15:49
    内容：Inventing the Service trait
        https://tokio.rs/blog/2021-05-14-inventing-the-service-trait
        这个算是tower的指引。。。主要是从无到有的讲解tower::Service,,,,  看了一部分，，， 待续。。。。
        Next: The Handler trait

## 第 201 个番茄时间
    时间：2022.05.01 18:54
    内容：Inventing the Service trait  (tower::Service的构建过程)
        https://tokio.rs/blog/2021-05-14-inventing-the-service-trait
        [The Handler trait]
        [Making Handler more flexible]
        [Backpressure]
        ```
        pub trait Service<Request> {
            type Response;
            type Error;
            type Future: Future<Output = Result<Self::Response, Self::Error>>;

            fn poll_ready(
                &mut self,
                cx: &mut Context<'_>,
            ) -> Poll<Result<(), Self::Error>>;

            fn call(&mut self, req: Request) -> Self::Future;
        }
        ```

## 第 202 个番茄时间
    时间：2022.05.02 01:07
    内容：https://docs.rs/axum/latest/axum/middleware/index.html
        看了一部分，，，  其实可能并非太久要，有点偏离第一性原则了。。。。

## 第 203 个番茄时间
    时间：2022.05.02 04:19
    内容：https://docs.rs/axum/latest/axum/middleware/index.html
        寥寥草草过一遍，，，，    我是个辣鸡，，，， 看得有点懵逼，，，，

## 第 204 个番茄时间(非标)
    时间：2022.05.02 13:48
    内容：axum数据库示例一瞥：
        sqlx-postgres : https://github.com/tokio-rs/axum/blob/main/examples/sqlx-postgres/src/main.rs
        tokio-postgres : https://github.com/tokio-rs/axum/blob/main/examples/tokio-postgres/src/main.rs

        postgresql的Schema是一个纯逻辑层面的概念，类似于“命名空间”的概念。。。

        这种资料乱翻，没法确定哪个更好，拍拍脑袋用：sqlx+postgres吧！！！

## 第 205 个番茄时间(非标)
    时间：2022.05.02 
    内容：https://github.com/tokio-rs/axum/blob/main/examples/sqlx-postgres/src/main.rs
        该示例涉及到tracing和tracing_subscriber的使用·~~

        https://github.com/tokio-rs/tracing/tree/master/tracing-subscriber

        没看明白~~~~


## 第 206 个番茄时间(非标)
    时间：2022.05.02 22:13
    内容：tracing & tracing_subscriber
        ```
        tracing_subscriber::registry()
            .with(tracing_subscriber::EnvFilter::new(
                std::env::var("RUST_LOG").unwrap_or_else(|_| "example_tokio_postgres=debug".into()),
            ))
            .with(tracing_subscriber::fmt::layer())
            .init();
        ```
        `tracing_subscriber::registry()` 返回一个结构体：tracing_subscriber::Registry。
        `with()` 是你属于tracing_subscriber::layer::SubscriberExt的函数，用于将 with(layer)组合到Subscriber中。

        `tracing_subscriber::EnvFilter::new(directives: S)` 返回一个 tracing_subscriber::filter::EnvFilter 。S 是逗号分隔的多个匹配Span和Event的directive。

        directive的表达式类似env_logger：`target[span{field=value}]=level`。

            - `target` 匹配event和span的目标，通常是模块路径和(或)crate的名称。比如：`h2`, `tokio::net`, or `tide::server`。
            - `span` 匹配 span的名称。
            - `field` matches on fields within spans.
            - `value` matches on the value of a span’s field.
            - `level` sets a maximum verbosity level accepted by this directive.

        `tracing_subscriber::fmt::layer()` 返回一个结构体 tracing_subscriber::fmt::Layer。 (默认配置)

## 第 207 个番茄时间(非标)
    时间：2022.05.03 11:36
    内容：搬运sqlx-postgres代码。。。。

        Send 和 Sync 属于 marker trait，几乎所有类型都默认实现了Send和Sync。
        Send 表示跨线程 move，Sync 表示跨线程 share data. 两者基本就是 ownership 和 borrow 的区别。
        Rc<T> 与 Arc<T> 的区别就在于：后者实现了Send和Sync，所以可以跨线程使用。

        常用两种方式使用数据库连接池： Extension作为extractor 和 自定义extractor？？？

## 第 208 个番茄时间(非标)
    时间：2022.05.03 14:58
    内容：打算先实现HTTP请求信息的数据库读写操作~
        请求来源IP、User-agent、URL、PATH、时间等，，，，

        请求包中的信息只能通过extractor来提取吗？？？？？？？

        参考： https://axum.rs/topic/roaming-axum/request

        略懵，，，， 待续。。。。。

## 第 209 个番茄时间(非标)
    时间：2022.05.03 17:19
    内容：打算先实现HTTP请求信息的数据库读写操作~

        OriginalUri提取器的使用：
        ```
        let app = Router::new()
            .nest("/api",get(|OriginalUri(original_uri): OriginalUri|async move {
                format!("Original Uri : {}",original_uri)
            }))
        ////////////////////////////////////
        async fn req_info(OriginalUri(original_uri): OriginalUri) -> String  {
            format!("Original Uri : {}", original_uri)
        }

        let app = Router::new().nest("/api",any(req_info))
        ```

        通过request extension来提取URL：OriginalUri 也可以通过请求扩展从middleware访问。
        粗浅的理解，Router::new().layer(service: S)的参数service就是所谓的中间件，实现了Service trait(内部实现poll_ready(), call()函数。。。)。
        
        在middleware内部使用 req.extensions().get::<OriginalUri>() 获得 url。

        继续懵逼，，，，，，，

## 第 210 个番茄时间(非标)
    时间：2022.05.03 20:56
    内容：https://axum.rs/topic/roaming-axum/request

        如何同时提取多个数据？ 
        提取的Header、IP、Path、参数等如何与数据库交互？逻辑代码写在哪里？？？？

        继续懵逼，，，，，，，

## 第 211 个番茄时间(非标)
    时间：2022.05.04
    内容：https://axum.rs/topic/roaming-axum/request
        https://axum.rs/topic/roaming-axum/cookie

## 第 212 个番茄时间(非标)
    时间：2022.05.05 12:25
    内容：https://axum.rs/topic/roaming-axum/response
        任何实现了IntoResponse trait的，都可以作为handler的返回值（即response 响应)

        后续可以关注下：https://github.com/tokio-rs/axum/discussions

## 第 213 个番茄时间(非标)
    时间：2022.05.06 00:20
    内容：https://axum.rs/topic/roaming-axum/response
        使用 layer()加入要共享的数据，使用Extension extractor在handler中取用数据？？？？


## 第 214 个番茄时间(非标)
    时间：2022.05.06 01:22
    内容：https://axum.rs/topic/roaming-axum/route        路由及路由嵌套
        https://axum.rs/topic/roaming-axum/middleware    中间件
            - 可以通过实现 `tower::Service` 来自定义中间件，但它非常复杂。
            - 可以通过`extractor_middleware()`方法，将一个 extractor 转成中间件。

## 第 215 个番茄时间(非标)
    时间：2022.05.06 11:48
    内容：https://axum.rs/topic/roaming-axum/postgres       axum 操作 Postgres 数据库
        相关源代码： https://github.com/axumrs/roaming-axum/blob/main/postgres/src/main.rs
        该示例中，数据库连接是直接在各个handler中call外部函数获得的，而非通过axum的状态共享获得。

## 第 216 个番茄时间(非标)
    时间：2022.05.06 23:52
    内容：https://axum.rs/topic/roaming-axum/redis          axum操作redis
        https://axum.rs/topic/roaming-axum/session         axum实现Session (with redis)  很好的例子！！！！

        相关源代码： https://github.com/axumrs/roaming-axum/blob/main/session/src/main.rs

## 第 217 个番茄时间(非标)
    时间：2022.05.07 00:55
    内容： https://axum.rs/topic/roaming-axum/config        axum配置文件

          同时使用了配置文件、Redis、postgresql：
          https://github.com/axumrs/roaming-axum/blob/main/config/src/main.rs

          https://axum.rs/topic/roaming-axum/error-handling    axum自定义extractor error。

        axum.rs的漫游系列浏览完了。。。。

        其他的实际项目，看起来还是不错的，可以作为参考。。。

        感觉又可以继续尝试写d2q项目的内容了。。。。

## 第 218 个番茄时间(非标)
    时间：2022.05.07 11:25
    内容： 规划接口功能。

## 第 219 个番茄时间(非标)
    时间：2022.05.07 15:55
    内容：  懵逼+发呆。。。
            tracing的levels: error > warn > info > debug > trace
            
        关于session，axum的Example代码中使用了async-session (https://github.com/http-rs/async-session)。

        可以考虑使用，以便后续直接将redis作为后端KV数据库使用。。。

        使用tracing::debug来打印http请求记录，应该如何实现？  通过中间件吗？

## 第 220 个番茄时间(非标)
    时间：2022.05.07 23:43
    内容：发现了官方的showcase。。。。。
        https://github.com/tokio-rs/axum/blob/main/ECOSYSTEM.md#project-showcase

        其中有一个showcase使用的技术栈是：axum+sqlx+postgresql. 非常值得借鉴。。。。
        https://github.com/launchbadge/realworld-axum-sqlx

        目前成功润起来了，，，，
        ```
        $ cargo install sqlx-cli --features postgres
        $ sqlx migrate run
        $ cargo run
        ```
        curl http://127.0.0.1:8080/api/users

        使用了下apifox，确实很不错的样子。。。。

## 第 221 个番茄时间(非标)
    时间：2022.05.08 17:20
    内容：继续研究 realworld-axum-sqlx
        再次浏览了以便《Programming Rust》第8章 包和模块。

        大概测试了realworld-axum-sqlx的user注册登录几个api。

## 第 222 个番茄时间(非标)
    时间：2022.05.08 22:40
    内容：
        https://cloak.software/blog/rust-on-nails   这个指导性项目也是  axum+sqlx+postgresql。
        
        看困了，，，，，，   

## 第 223 个番茄时间(非标)
    时间：2022.05.09 08:59
    内容：
        vs code的 Remote-Container兔子洞待了一会儿，，，  
        总结起来就两种常见可能比较使用：具有高性能服务器主机；开发环境安全隔离。

        接下来还是直接阅读cloak的源代码好些：
        https://github.com/purton-tech/cloak

## 第 224 个番茄时间(非标)
    时间：2022.05.10
    内容：cloak项目比较复杂，打算还是先按着其blog操作运行起来看看。。。

        能跟着稍微学习vscode远程开发，还是可以的。。。

## 第 225 个番茄时间(非标)
    时间：2022.05.11 21:00
    内容：
        https://cloak.software/blog/rust-on-nails   继续

## 第 226 个番茄时间(非标)
    时间：2022.05.11 22:30
    内容：https://cloak.software/blog/rust-on-nails  
        省略的内容越来越多了，看不太明白了。。。。
        算了，还是开始搞自己的项目好一点，这个反倒是复杂的一批。。。  涉及太多别的内容。。。

        build.rs到底是干什么用的呢？
        Cargo 就会先编译和执行build.rs，然后再去构建整个项目！！！

## 第 227 个番茄时间(非标)
    时间：2022.05.14 23:14
    内容：d2q项目，将之前测试的函数移动到了独立的mod。

## 第 228 个番茄时间(非标)
    时间：2022.05.16 00:29
    内容：d2q项目ing

## 第 229 个番茄时间(非标)
    时间：2022.05.17 00:15
    内容：d2q项目ing
        怎么优雅的初始化数据库/表？？？

## 第 230 个番茄时间(非标)
    时间：2022.05.23 23:44
    内容：d2q项目ing
        不使用anyhow就不能够正常运行吗？  return值待回顾学习。。。

## 第 231 个番茄时间(非标)
    时间：2022.05.25 22:27
    内容：d2q项目ing      
        需要自定义error。。。。。
        error 也需要实现IntoResponse

## 第 232 个番茄时间(非标)
    时间：2022.05.27 00:52
    内容：d2q项目ing      
        thiserror  ---> 派生宏。
        thiserror::Error
        ```
        #[derive(Error)]
        {
            // Attributes available to this derive:
            #[backtrace]
            #[error]
            #[from]
            #[source]
        }
        ```
        感觉为了看懂`realworld-axum-sqlx`都不是那么简单的事情。。。。。

## 第 233 个番茄时间(非标)
    时间：2022.06.18 15:00
    内容： 细说Rust错误处理  https://rustcc.cn/article?id=75dbd87c-df1c-4000-a243-46afc8513074
        
        所以，这就是为什么都推荐使用anyhow / thiserror吗？

        anyhow: Flexible concrete Error type built on std::error::Error
        thiserror: derive(Error) for struct and enum error types


## 第 234 个番茄时间(非标)
    时间：2022.06.30 00:12
    内容： 关于 Rust 错误处理的思考     https://rustmagazine.github.io/rust_magazine_2021/chapter_2/rust_error_handle.html

        对于一些新的错误处理库，目前社区里较为主流的建议可能是组合使用 thiserror 和 anyhow 这两个库。其中 thiserror 可以看作是定义 Error 的一个工具，它只帮你生成一些定义 Error 的代码，别的什么都不做，相当纯粹。
        而 anyhow 则为你定义好了一个 Error 类型，基本可以看作是一个 Box<dyn Error> ，同时还提供了一些如 context 等扩展功能，用起来更加无脑。

        snafu 是更好的选择？？？

## 第 235 个番茄时间(非标)
    时间：2022.07.14 14:22
    内容： 重读https://github.com/launchbadge/realworld-axum-sqlx。
        遇到cargo.toml文件中clap未启用derive特性导致的报错问题。

## 第 236 个番茄时间(非标)
    时间：2022.07.15 14:33
    内容： 重读https://github.com/launchbadge/realworld-axum-sqlx。
        good job, str和闭包的知识忘了，，，，，   

## 第 237 个番茄时间(非标)
    时间：2022.07.15 15:51
    内容： 闭包~
        fn(&City) -> bool // fn类型(仅函数)
        Fn(&City) -> bool // Fn特型(包括函数和闭包)

        闭包可以调用，但它不是 fn。
        每个闭包都有自己的类型，因为闭包可能包含(从包含作用域中借来或偷 来的)数据。这可能是任意多个变量，这些变量也可能是任何类型。因此编译器会为每个 闭包创建一个临时类型，大到足以存储它的数据。任何两个闭包的类型都不相同。但所有 闭包都会实现 Fn 特型。
        由于每个闭包都有自己的类型，因此使用闭包的代码通常需要是泛型的。

## 第 238 个番茄时间(非标)
    时间：2022.07.15 17:55
    内容： 
        let app = Router::new().route("/", get(|| async { "Hello, World!" }));

## 第 239 个番茄时间
    时间：2022.07.22 22:49
    内容： 
        回过头翻了翻之前关于axum的笔记。。。
        待继续。。。

## 第 240 个番茄时间
    时间：2022.07.25 02:03
    内容： 困死了。。。。
        继续看“中间件”相关。。。
        
## 第 241 个番茄时间
    时间：2022.07.25 13:52
    内容： go ahead....

## 第 242 个番茄时间
    时间：2022.07.25 
    内容： Cow类型，Clone-on-write，可以同时存储Owned类型或者Borrowed类型，在对内容进行修改时进行Clone，否则就只借用。
        Error枚举需要实现 IntoResponse 特型。

## 第 243 个番茄时间
    时间：2022.07.25 18:45
    内容： go on....

## 第 244 个番茄时间
    时间：2022.07.26 18:12
    内容： 
        axum 0.5版本相对于0.3版本有变动，故而在realworld-axum-sqlx代码存在变动。
        
        https://tokio.rs/blog/2022-03-whats-new-in-axum-0-5

        下一步：看看怎么给自定义错误类型添加 IntoResponse trait。

## 第 245 个番茄时间
    时间：2022.07.27 11:46
    内容： 
        因为axum 0.5 版本差异，所以相关的学习，最好还是看官方原始文档。
        error_handling的核心目的就是让error类型实现Infallible。（功能意义上错误，但代码意义上要正确的处理错误。。。。）
        https://docs.rs/axum/latest/axum/error_handling/index.html

        next: 阅读 IntoResponse 相关内容。

## 第 246 个番茄时间
    时间：2022.07.27 15:37
    内容：
        看了一丢丢 IntoResponse，解决了d2q上的一个小问题。。。。

        待续。。。

## 第 247 个番茄时间
    时间：2022.07.27 17:31
    内容：
        axum::response::IntoResponseParts  了解一二。。。。

        next: 继续完善d2q

## 第 248 个番茄时间
    时间：2022.07.28 11:41
    内容：
        sqlx database reset
        sqlx migrate add user    // 貌似只生成了一个空文件，具体的SQL语句需要自行填入。

        next: 暂停折腾数据库，先把用户的增删改查功能实现。。。。

## 第 249 个番茄时间
    时间：2022.07.28 
    内容：
         echo -n "examplepass" | openssl dgst -sha256     --->   7437de75202124dc8370ee1c167712074c395d6db64f8266d04412f8adfa0a46
         
## 第 250 个番茄时间
    时间：2022.07.28 18:18
    内容： String 与 &str
        https://blog.thoughtram.io/string-vs-str-in-rust/  https://zhuanlan.zhihu.com/p/123278299
        
        因为rust的解引用强制转换（deref coercions）特性，使得 &String 自动转换为 &str。

## 第 251 个番茄时间
    时间：2022.07.28 23:43
    内容： 
        rust 加密生态： ring, rustls。
        rust hash库： https://github.com/RustCrypto/hashes
        sha2: https://docs.rs/sha2/latest/sha2/

        let mut hasher = Sha512::new();
        hasher.update(password_tmp);
        let result = hasher.finalize();

        result是Box<[u8]>类型，如何转换为String呢？？？？？

## 第 252 个番茄时间(非标)
    时间：2022.07.29 16:36
    内容： 
        sha512的哈希值太长了，求其次用sha512_256好了。 (在64位CPU的平台上，sha512比sha256快)。

        对于具有名称不可重复的自然特性的对象，最好使用Version 3/5的UUID。比如系统中的用户。

        除了使用push_str来拼接字符串外，有时候直接用 Add 运算符更好。

        next: create_user 写数据到数据库。

## 第 253 个番茄时间(非标)
    时间：2022.07.29 18:33
    内容： 
        生成uuid。

        next: sqlx insert操作。。。。

## 第 254 个番茄时间(非标)
    时间：2022.07.30 11:33
    内容： 
        使用 sqlx::query_scalar! 执行了insert。

        next: 研究下 on_constraint 的实现。。。。

## 第 255 个番茄时间(非标)
    时间：2022.07.30 15:44
    内容：  
        用户登录功能实现。。。  整体存在问题：请求和响应包的毫无设计可言，混乱不堪。

        next: 引入JWT，用户更新及信息获取。

## 第 256 个番茄时间(非标)
    时间：2022.07.31
    内容：
        初略阅读了一些关于JWT相关的内容，，，

        next: jwt代码实践。。。。。

## 第 257 个番茄时间(非标)
    时间：2022.08.02 18:56
    内容：
        axum::extract::FromRequest 貌似有变动。。。
        
        #[async_trait] 又是什么鬼。。。。
        
        亟待研究下extractor的写法。。。

## 第 258 个番茄时间(非标)
    时间：2022.08.03
    内容：
        jwt长度瘦身：简化Claims的字段名称及内容长度；使用更短的哈希算法。
        从当前版本的jwt代码来看，貌似只支持Sha256,Sha384,Sha512，分别对应Hs256,Hs384,Hs512。

        jwt中payload可能会信息泄漏，怎么处理？

## 第 259 个番茄时间(非标)
    时间：2022.08.03 15:31
    内容：
        实现在login的时候，更新user表中的last_login_at字段。
        ```
        if user.credential == credential {
            // update the last login datetime
            let update_result = sqlx::query!(
            // language=PostgreSQL
            r#"
                update "user"
                set last_login_at = now()
                where uuid = $1
            "#,
            &user.uuid
        )
                .execute(&ctx.db)
                .await?;
        ```

## 第 260 个番茄时间(非标)
    时间：2022.08.03 17:16
    内容：复合用户创建与用户更新方法。

        电脑没电了，待完善，，，，
        
## 第 261 个番茄时间(非标)
    时间：2022.08.03 21:38
    内容：勉强完成了用户的更新，，，    整体而言，代码功能上还存在问题的。。。

## 第 262 个番茄时间(非标)
    时间：2022.08.04 
    内容：Memo数据表设计~
        Memo名，触发类型、触发条件、终止条件
        ```
        create table if not exists memo
        (
            uuid              uuid not null constraint memo_pk primary key,
            user_uuid         uuid not null,
            memoname          text not null,
            description       text,
            trigger_type      integer,
            trigger_condition text,
            termination_times integer,
            is_delete         boolean default false,
            create_at         timestamp with time zone,
            update_at         timestamp with time zone
        );

        create unique index if not exists memo_uuid_uindex
            on memo (uuid);
        ```

## 第 263 个番茄时间(非标)
    时间：2022.08.04 16:22
    内容：
        做好了memo::router()。

## 第 264 个番茄时间(非标)
    时间：2022.08.05 00:31
    内容：
        在设计Memo相关的响应包时，设计了结构体
        ```
        #[derive(serde::Serialize)]
        struct MemoResponse {
            state: bool,
            msg: Option<String>,
            data: Option<MemoResponseData>,
        }
        ```,
        其中MemoResponseData原本尝试使用联合体union类型，但总是报错，可能跟Copy trait, ManuallyDrop什么的有关，，，，  

        改用enum类型，貌似可以解决问题。。
        ```
        #[derive(serde::Serialize)]
        enum MemoResponseData {
            memolist(Vec<String>),
            memodetail(Memo),
        }
        ```

        handler函数中响应：
        ```
        Ok(Json(MemoResponse{state: true, msg: None,
            data: None,
            // data: MemoResponseData::memodetail(Memo{memoid: Some("123123".to_string()),..Default::default()})
            // data: Some(MemoResponseData::memolist(vec!["1234".to_string(),"5678".to_string(),"1100".to_string()]))
        }))
        ```

        next: 完善create_update_memo的功能。。。。

## 第 265 个番茄时间(非标)
    时间：2022.08.05 12:32
    内容：

        写了 create_update_memo() update部分代码，尚未验证正确性。

        next: 继续

## 第 266 个番茄时间(非标)
    时间：2022.08.05 15:02
    内容：
        有错误。。。。

## 第 267 个番茄时间(非标)
    时间：2022.08.05 17:12
    内容：
        ```
        async fn create_update_memo(
            auth_user: AuthUser,
            Json(memo): Json<Memo>,
            ctx: Extension<ApiContext>,
        ) -> Result<Json<MemoResponse>> {
            let memo_uuid = Uuid::try_parse(&memo.memoid.unwrap_or(String::new()))?;
            // 此处 ? 返回的错误类型是：Uuid::Error，是不同于 D2qErr的，该如何处理呢？

            Err(D2qErr::NotFound)
        }
        ```

        当前解决办法：
        在error.rs中：
        ```
        #[derive(thiserror::Error, Debug)]
        pub enum D2qErr {
            
            #[error("an internal server error occurred")]
            Anyhow(#[from] anyhow::Error),

            #[error("an uuid error occurred")]
            Uuid(#[from] uuid::Error),
        }
        ```

        触发报错时：直接返回“an uuid error occurred”。 

        本质上应该是用anyhow来实现的From<T> trait。

        展示放过，以后需要进一步学习及优化。

## 第 268 个番茄时间(非标)
    时间：2022.08.05 18:41
    内容：
        going...

## 第 269 个番茄时间(非标)
    时间：2022.08.06 01:08
    内容：
        设计Memo记录的消极表、积极表
        ```sql
        create table if not exists quitmemo
        (
            uuid       uuid                               not null
            constraint memo_quitrecord_pk
            primary key,
            memo_uuid  uuid                               not null,
            quit_time  timestamp with time zone default now(),
            quit_level integer                  default 1 not null,
            quit_type  text,
            quit_desc  text
            );

        comment on table quitmemo is '所有过程中或主观或客观原因造成的放弃。';

        comment on column quitmemo.quit_level is '消极情绪的级别：1-一般，2-高，3-严重。';

        comment on column quitmemo.quit_type is '原因：怠惰，挫败，焦虑，烦躁，贪玩，没时间，，，';

        create unique index if not exists memo_quitrecord_uuid_uindex
            on quitmemo (uuid);
        ------------------------
        create table if not exists staymemo
        (
            uuid      uuid not null
            constraint staymemo_pk
            primary key,
            memo_uuid uuid not null,
            stay_time timestamp with time zone default now(),
            stay_desc text
            );

        comment on table staymemo is '所有积极的付出';

        create unique index if not exists staymemo_uuid_uindex
            on staymemo (uuid);
        ```

## 第 270 个番茄时间(非标)
    时间：2022.08.06 11:57
    内容：
        chrono 库是time库的超集。

        create_quitrecd 又报错，，，，，

## 第 271 个番茄时间(非标)
    时间：2022.08.06 14:18
    内容：
        sqlx::query! select返回值的处理有点麻烦的样子，，，
        ```
        let validmemocount;
        match sql_result.validmemocount{
            Some(vvv) => validmemocount = vvv,
            _ => validmemocount = 0,
        }
        ```

        在rust中，如果中途return，需要加return关键字。。。

## 第 272 个番茄时间(非标)
    时间：2022.08.06 21:03
    内容：

        sqlx返回大量结构体，如何进行批量重整呢？

        ```
        let quitrecdlist = sqlx::query_as!(
            QuitRecordFromQuery,
            r#"
                select uuid as record_uuid, memo_uuid, quit_time, quit_type, quit_level, quit_desc from quitrecord
                where memo_uuid = (select uuid from memo where user_uuid = $1 and uuid = $2 and is_delete = false)
            "#,
            user_uuid,
            memo_uuid
        )
            .fetch_all(&ctx.db)
            .map_ok(QuitRecordFromQuery::into_quitrecord)
            .try_collect()
            .await?;
        ```

        遇到苦难呢了。。。。

## 第 273 个番茄时间(非标)
    时间：2022.08.07 02:19
    内容：
        如此进行转换，，，，，
        ```
        let newquitrecdlist: Vec<QuitRecord> = quitrecdlist.into_iter()
                .map(|x|x.into_quitrecord())
                .collect();
        ```

        至此，record的创建及查询功能完成。。。。

        next: 前端代码的实现。。。。

        next next: 前端作为需求，驱动后端代码改进。。。

## 第 274 个番茄时间(非标)
    时间：2022.08.07 
    内容：
        taro cli安装，，，，，  
        taro 项目初始化
        ```bash
        $ taro init w2qweb

        ? 请输入项目介绍 d2quit web端
        ? 请选择框架 Vue3
        ? 是否需要使用 TypeScript ？ Yes
        ? 请选择 CSS 预处理器（Sass/Less/Stylus） Sass
        ? 请选择编译工具 Webpack5
        ? 请选择包管理工具 yarn
        ? 请选择模板源 Gitee（最快）
        ✔ 拉取远程模板仓库成功！
        ? 请选择模板 vue3-NutUI（使用 NutUI3.0 的模板）
        ```
        
## 第 275 个番茄时间(非标)
    时间：2022.08.07 23:38
    内容：
        兔子洞 taro --> vue3 --> typescript

        了不起的 TypeScript 入门教程（1.2W字）
        https://segmentfault.com/a/1190000022876390


        TypeScript: TS Playground
        https://www.typescriptlang.org/play

        Next: 快速过一遍TS，酌情看要不要过过JS，然后过vue3。
        


## 第 276 个番茄时间(非标)
    时间：2022.08.08 18:42
    内容：
        ```
        var Direction;   是变量声明

        Direction = {}  是变量赋初始值

        然后函数体内对参数的修改，可以影响外部变量~~~
        ```

        any 和 unknown 的最大区别是, unknown 是 top type (任何类型都是它的 subtype) , 而 any 即是 top type, 又是 bottom type (它是任何类型的 subtype ) ,这导致 any 基本上就是放弃了任何类型检查.

        可以使用 as 关键字将 unknown强制转换为具体类型，再进行操作。   该方式存在问题。。。

        可以使用 typeof，instanceof 来缩小变量的类型。   此方法称为： 类型收缩。
        ```
        type getAnimal = () => unknown;

        const dog = getAnimal();
        
        if (dog instanceof Dog) {
        console.log(dog.name.toLowerCase());
        }
        ```





--------------------
时常检视“第一性原则”!!!!
