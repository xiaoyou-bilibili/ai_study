> Tmux 是一款可以管理会话和分屏的终端复用器。在远程 SSH 断开后可以继续执行任务，重新连接后再继续会话。也能够将进程放到后台运行，需要时重新接管。为了防止 SSH 因网络断开造成的进程运行中断，推荐把所有需要长期运行的训练等任务都使用 Tmux 终端。

```shell
# 创建一个新的终端
tmux new -s session1
# 当需要退出该会话，将会话放在后台运行时，可以使用下面这个命令，或使用快捷键 Ctrl + B，再按 D 来退出会话。
tmux detach
# 查看所有回话
tmux ls
# 恢复某个对话
tmux a -t session1
# 删除指定会话
tmux kill-session -t session1
# 删除所有会话
tmux kill-server
```
