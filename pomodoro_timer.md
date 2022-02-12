
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
        通过特征对象实现的代码相比于泛型的，少了一些代码肿胀(code bloat)。
        一般地，泛型更具有优势：不使用dyn关键词(没有涉及特征对象）因此不涉及动态调度，故而运行速度更快。