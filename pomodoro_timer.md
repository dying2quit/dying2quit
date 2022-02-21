
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

## 第 063 个番茄时间

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

## 第 064 个番茄时间

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
        
## 第 065 个番茄时间

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

## 第 066 个番茄时间

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

## 第 067 个番茄时间

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

## 第 068 个番茄时间

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

## 第 069 个番茄时间

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

## 第 070 个番茄时间

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

## 第 071 个番茄时间

    时间：2022.02.20 00:15
    内容：《Programming Rust 2nd Edition》第313-315页。
        [Utility Traits] - Default
        如果结构体的各字段都实现了Default，则可以使用#[derive(Default)]自动实现结构的默认值。

        [Utility Traits] - AsRef and AsMut
        如果一个类型实现了AsRef<T>，则可以有效地借用一个&T。AsMut -----> &mut T

        AsRef通常用于使函数在接受参数的类型中更加灵活。如此，任何实现了AsRef<T>的类型都可以被接受。

## 第 072 个番茄时间

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

## 第 073 个番茄时间

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

## 第 074 个番茄时间

    时间：2022.02.20 17:26
    内容：《Programming Rust 2nd Edition》第320-321页。
        From和Into转化可能比AsRef和AsMut需要更多的开销。
        ？运算符使用From和Into来帮助清理可能以多种方式失败的函数中的代码，方法是在需要时自动从特定的错误类型转换为常规错误类型。

        From和Into是绝对可靠的trait。  wrapping转换？  saturating(饱和)转换？

        [Utility Traits] - From and Into
        对于不确定如何转化为妥的情形，Rust中实现复杂一些的TryFrom和TryInto来替代From和Into。 对应的方法是：try_from() 和 try_into()。

## 第 075 个番茄时间

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

## 第 076 个番茄时间

    时间：2022.02.20 21:40
    内容：《Programming Rust 2nd Edition》第323-324页。
        [Utility Traits] - Borrow and ToOwned at Work: The Humble Cow     写时复制 / 写时克隆 -- 避免不必要的复制。
        函数参数接收值还是引用？ 这是一个问题～～～～，可用Cow类型来解决～  Clone-on-write，即写时克隆。本质上是一个智能指针。

        https://wiki.jikexueyuan.com/project/rust-primer/intoborrow/cow.html

        写时复制（Copy on Write）技术是一种程序中的优化策略，多应用于读多写少的场景。主要思想是创建对象的时候不立即进行复制，而是先引用（借用）原有对象进行大量的读操作，只有进行到少量的写操作的时候，才进行复制操作，将原有对象复制后再写入。这样的好处是在读多写少的场景下，减少了复制操作，提高了性能。

        -------------------------
        Rust的诸多trait仍旧不懂～～～～～

## 第 077 个番茄时间

    时间：2022.02.21 10:03
    内容：《Programming Rust 2nd Edition》第325-327页。
        [CHAPTER 14 -- Closures]
        [Closures - Capturing Variables]
        变量捕获～～～

## 第 078 个番茄时间

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

## 第 079 个番茄时间

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



## 第 080 个番茄时间

    时间：2022.02.21 
    内容：《Programming Rust 2nd Edition》第333-页。
