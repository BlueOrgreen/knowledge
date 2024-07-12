
# 之后需要统一整理到我的博客当中

# tree 命令

**tree** 命令可以显示当前文件夹的目录结构

**-I** 命令可以使用正则来排除不想要的文件夹

```bash
tree -I "node_modules"
```


# 进程 命令

```bash
# 查看端口号占用进程
lsof -i [端口号]  # Mac系统
netstat -ano | findstr [端口号]  # window 系统


# 杀掉进程
kill -9 [端口号]  # Mac 系统
taskkill /f /t /im [端口号] # Window系统

```