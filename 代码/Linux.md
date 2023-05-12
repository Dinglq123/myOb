# Anaconda安装
[这是参考链接](https://blog.csdn.net/qq_53564294/article/details/120535377)
# screen
```shell
# 创建窗口web
screen -S web
# 列出所有
screen -ls
# 断开当前窗口(继续运行)
键入 ctrl + a + d

# 对于正在启动的后台进程修改名字
screen -S 原始任务名 -X sessionname 修改后的任务名

# 退出当前窗口
exit

# 关闭当前 windows
ctr + a + k
# 切换上一个 windows
ctr + a + p
# 给 windows 命名
ctr + a + A
# 显示所有 windows
ctr + a + w

# 通过编号索引 windows
ctr + a + 数字



# 左右分屏（‘或’的符号）
ctrl+a, |

# 切换屏幕
ctrl+a, tab

# 创建新窗口（以及改名）
ctrl+a, c

# 上下分屏（以及改名，切换屏幕，创建新窗口）
ctrl+a, S

# 关闭当前焦点所在的屏幕区块
ctrl+a, X

# 关闭除当前区块之外其他的所有区块
ctrl+a, Q

```