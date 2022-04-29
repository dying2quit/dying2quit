## 问题点


- (2022.01.05) 与“戒烟”过程中的”放弃作为“相反，本项目的关键是要“放弃不作为“（戒怠惰情绪），所以在操作上明显不适用。

    > 确实存在严重的场景不符合性，“戒惰”比较虚无缥缈，尝试每一次“戒惰”记录附带一个“番茄时间”？ 如此一来是否就变得没有意义了？ 

    尽管如此，还是先试试看吧。 番茄就番茄吧！ 先把rust书籍看完。。。

- (2022.01.05) 下班回家刷了好几个小时的抖音，压根没法提起学习欲望。感觉要废了～～～   如此一样，这个项目多少是有点憨憨了。

- (2022.01.08) 大家都这么看好Rust，有没有可能是大家都被虐的很惨，不敢承认自己呆，故而无限吹捧之？

- (2022.01.15) 太怕社死，将commit中的信息修改下。。。
    使用如下命令批量执行。。。。   git rebase -i ; git commit -amend 的方式太慢了，一个一个弄～～～
    ```
        git filter-branch -f --env-filter '
        OLD_EMAIL="dying2quit@example.com"
        CORRECT_NAME="quit"
        CORRECT_EMAIL="dying2quit@example.com"
        if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
        then
            export GIT_COMMITTER_NAME="$CORRECT_NAME"
            export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
        fi
        if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
        then
            export GIT_AUTHOR_NAME="$CORRECT_NAME"
            export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
        fi
        ' --tag-name-filter cat -- --branches --tags
    ```

- (2022.01.15) 考虑开发小程序需要用到web框架，各种框架一堆堆，戳的我这个选择困难症痛苦不堪，也许直接使用hpyer会更好。

- (2022.01.16) 鉴于axum最新最火，后续可尝试用这个框架。 axum涉及的东西还是蛮多的，包括tower,hyper,tonic等，所以还是先把Programming Rust过完，再研究axum。

- (2022.01.20) 在开发过程中一定会用到数据库连接库，经搜索发现主要有r2d2和bb8两种库，网络上的评论认为bb8比r2d2好一些。axum示例中也使用的是bb8。

- (2022.02.18) 找出了之前买的《Programming Rust》中文版（第一版），发现还是中文的阅读速度快很多啊。  唯一的痛点就是内容略旧，也可能存在勘误。

- (2022.02.21) 目前这样的学习模式效率太低了，应该尽快跳过基础知识的学习，进入实践学习的过程。

- (2022.03.24) 最先实现一个具备CRUD的API-DB功能。  axum -- sqlx? -- postgresql

- (2022.04.29) 本已经开始准备啃小程序，但看了之前的note，干脆还是搞个最简单的：web版本。(前后端分离，H5前端taro，后端axum，数据库postgresql)。 先学习一下axum。

