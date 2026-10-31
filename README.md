# hello-github

> 用于验证 **WorkBuddy × GitHub** 工作链路的演示仓库。

## 这个文件是怎么写进来的

由 WorkBuddy 在本机通过 **SSH 密钥**认证后 `git push` 提交，全程没有人工敲命令。

## 链路验证记录

| 能力 | 通道 | 结果 |
|---|---|---|
| 读取账号信息 | GitHub 连接器 | 通过 |
| 读取公有仓库文件 | GitHub 连接器 | 通过 |
| 读取私有仓库文件 | GitHub 连接器 | 失败（404，无访问权） |
| 新建仓库 | GitHub 连接器 | 失败（403 Resource not accessible by integration） |
| 写入已有仓库文件 | GitHub 连接器 | 失败（403 Resource not accessible by integration） |
| 克隆仓库 | 本地 git + SSH | 通过 |
| 提交并推送 | 本地 git + SSH | 通过 |

## 结论

GitHub 连接器在本会话中**只读**（对已授权公有仓库），建仓与写入均被 GitHub App 权限拦截。

**写操作走本地 git + SSH 通道**，稳定、不受连接器权限影响，已配置完成：

- 密钥：`~/.ssh/id_ed25519`（ed25519，无口令）
- 身份：`langzhuwei <langzhuwei@users.noreply.github.com>`
- 默认分支：`main`

## 后续可做的事

- 把本地项目推到这里或新建仓库
- 用连接器做只读检索：搜代码、看 PR、读 Issue
- 写操作用 git，读操作用连接器，各取所长
