
# 之后需要统一整理到我的博客当中

## tree 命令

**tree** 命令可以显示当前文件夹的目录结构

**-I** 命令可以使用正则来排除不想要的文件夹

```bash
tree -I "node_modules"
```


## 进程 命令

```bash
# 查看端口号占用进程
lsof -i [端口号]  # Mac系统
netstat -ano | findstr [端口号]  # window 系统


# 杀掉进程
kill -9 [端口号]  # Mac 系统
taskkill /f /t /im [端口号] # Window系统

```

[多版本node工具](https://volta.sh/)


## Nvm

`nvm` 切换失败

```bash
# 执行命令
source ~/.nvm/nvm.sh

# 放置于 .zshrc 中

```json
{
    "volta": {
        "node": "20.15.0",
        "yarn": "1.22.22"
    }
}
```


curl 调接口 并且通过 json 可以将数据json化 方便查看

```bash
npm i -g json
curl [xxx] | json
```