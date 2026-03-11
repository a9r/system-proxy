# proxy.sh

Linux 代理一键管理脚本，交互式为常用工具开启或关闭代理。**自动检测已安装的组件**。

## 快速使用

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/a9r/system-proxy/refs/heads/main/proxy)
```

## 主菜单

```
╔══════════════════════════════════╗
║      Linux 代理一键管理脚本      ║
╚══════════════════════════════════╝

  代理地址: http://127.0.0.1:7890

  1)  开启代理（交互式选择组件）
  2)  关闭代理（交互式选择组件）
  3)  查看当前状态
  q)  退出
```

选择开启或关闭后，进入组件选择界面，输入序号（空格分隔多个）或 `a` 全选。

## 组件菜单示例

只显示当前系统**已安装**的组件，例如 Debian 系统不会出现 YUM：

```
  序号  组件              状态
  ─────────────────────────────────────────
  1)    系统环境变量      [未设置]
  2)    Docker           [已开启]
  3)    APT              [未设置]
  4)    NPM              [未设置]
  5)    GIT              [已开启]
  6)    WGET             [未设置]
  ─────────────────────────────────────────
  a)    全选
  q)    返回主菜单
```

## 修改代理地址

编辑脚本开头的两个变量：

```bash
PROXY_HOST="127.0.0.1"
PROXY_PORT="7890"
```

## 支持的组件

| 组件 | 配置文件 |
|------|---------|
| 系统环境变量 | `/etc/environment` |
| Docker | `/etc/systemd/system/docker.service.d/http-proxy.conf` |
| YUM | `/etc/yum.conf` |
| APT | `/etc/apt/apt.conf.d/95proxy` |
| NPM | `~/.npmrc` |
| PIP | `~/.pip/pip.conf` |
| GIT | `~/.gitconfig` |
| WGET | `/etc/wgetrc` |

## 注意事项

- 执行需要 `sudo` 权限
- 开启代理前自动检测连通性，不可用时返回主菜单
- 系统环境变量修改后需**重新登录 shell** 生效
