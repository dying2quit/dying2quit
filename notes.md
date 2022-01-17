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

- (2022.01.16) 鉴于axum最新最火，后续可尝试用这个框架。 