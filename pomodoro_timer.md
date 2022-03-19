
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



-------------
███████╗██████╗ ███████╗███████╗██████╗     ██╗   ██╗██████╗  
██╔════╝██╔══██╗██╔════╝██╔════╝██╔══██╗    ██║   ██║██╔══██╗ 
███████╗██████╔╝█████╗  █████╗  ██║  ██║    ██║   ██║██████╔╝ 
╚════██║██╔═══╝ ██╔══╝  ██╔══╝  ██║  ██║    ██║   ██║██╔═══╝  
███████║██║     ███████╗███████╗██████╔╝    ╚██████╔╝██║      
╚══════╝╚═╝     ╚══════╝╚══════╝╚═════╝      ╚═════╝ ╚═╝      


