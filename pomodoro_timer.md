
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

    时间：2022.01.13 01:
    内容：https://rustwiki.org/zh-CN/book/ch15-02-deref.html
        当所涉及到的类型定义了 Deref trait，Rust 会分析这些类型并可以任意多次调用 Deref::deref方法以获得匹配参数的类型。
        DerefMut trait 用于重载可变引用的 * 运算符。
        当 T: Deref<Target=U> 时从 &T 到 &U。
        当 T: DerefMut<Target=U> 时从 &mut T 到 &mut U。
        当 T: Deref<Target=U> 时从 &mut T 到 &U。
        ---------------
        Drop trait是智能指针第二个重要的trait，允许我们在值要离开作用域时执行一些代码（drop方法）。未完待续。。。

