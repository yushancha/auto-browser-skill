# 自动浏览器 Skill

装上后只需要在 Claude Code 进入你所在想进入的浏览器，来浏览、操控你的浏览器，并发消息、查看邮箱。

## 功能特性

- 🤖 自动执行浏览器操作
- 🔍 支持搜索X(Twitter)、Google、百度等平台
- 📕 支持小红书发笔记、查看消息
- 🐟 支持咸鱼回复买家、查看订单
- 📧 可以查看和操作邮箱
- 📱 支持各种网页自动化任务
- 🔐 使用本地已登录的浏览器账号
- 💬 可以帮你回复消息
- ⚡ 支持24小时自动回复脚本

## 快速开始

### 第一步：安装 Claude Code

如果没有安装 Claude Code，先去官网下载安装：
👉 [https://claude.com/download](https://claude.com/download)

### 第二步：安装 Playwright MCP（复制下面命令即可）

**Windows 用户复制这个命令：**
```
npx -y @anthropic-ai/playwright
```

**Mac/Linux 用户复制这个命令：**
```
npx -y @anthropic-ai/playwright
```

安装方法：
1. 打开 Claude Code
2. 按 `Ctrl + Shift + P`（Windows）或 `Cmd + Shift + P`（Mac）
3. 输入 "MCP" 找到 "MCP Servers: Add"
4. 选择 "Playwright"
5. 在 Command 里粘贴上面的命令：`npx -y @anthropic-ai/playwright`
6. 点击保存，Claude Code 会自动下载安装

或者直接告诉 Claude Code："请帮我安装 Playwright MCP"，然后复制上面的命令给它。

### 第三步：安装 Skills

1. 下载本项目的 `SKILL.md` 文件
2. 复制到你的 Claude Code skills 目录：
   - **Windows**: `C:\Users\你的用户名\.claude\skills\`
   - **Mac/Linux**: `~/.claude/skills/`

### 第四步：配置你自己的浏览器账号

打开 `SKILL.md`，找到"浏览器配置信息"部分，修改以下内容：

```bash
# 将这些占位符替换成你自己的信息
<你的Chrome路径>           → 你的Chrome安装路径
<你的用户数据目录>         → 你的浏览器用户数据目录
<你的用户名>              → 你的X用户名
<你的Profile>             → 你的浏览器Profile编号
```

## 使用示例

### X (Twitter) 相关

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开我的X账号" | 打开你配置的X主页 |
| "打开X搜索归藏" | 打开X搜索归藏并进入主页 |
| "进入归藏主页" | 进入归藏的主页查看他今天发的内容 |
| "查看今天发了什么" | 进入主页查看最新帖子 |
| "帮我发一条X笔记" | 打开发帖子界面 → 输入内容 → 发布 |
| "帮我回复这条消息" | 打开消息 → 阅读内容 → 回复 |

### 小红书相关

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开小红书" | 打开小红书网页版 |
| "帮我发小红书笔记" | 打开发布笔记界面 → 输入内容/图片 → 发布 |
| "查看小红书消息" | 打开消息中心查看评论、点赞等 |

### 咸鱼相关

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开咸鱼" | 打开咸鱼网页版 |
| "帮我回复买家消息" | 打开消息中心 → 回复买家咨询 |
| "查看今天的新订单" | 进入订单页面 → 查看新订单 |

### 邮箱相关

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开邮箱" | 打开Gmail或其他邮箱 |
| "查看最新邮件" | 查看收件箱最新邮件 |
| "回复这封邮件" | 打开邮件 → 阅读内容 → 回复 |

### 24小时自动回复（进阶功能）

如果想要24小时自动回复消息，需要写一个自动回复脚本：

**直接告诉 Claude Code**："请帮我写一个自动回复脚本"

Claude 会用自然语言和你对话，了解你的需求后帮你创建脚本，例如：
- 自动回复 X 粉丝消息
- 自动回复咸鱼买家咨询
- 自动回复小红书评论

**运行脚本**：让脚本在后台运行，保持浏览器在线即可实现24小时自动回复

## 详细安装教程

### 方法一：通过 Claude Code 设置界面安装 MCP

1. 打开 Claude Code
2. 点击左下角的设置图标 ⚙️
3. 点击 "MCP Servers"
4. 点击 "Add MCP Server"
5. 输入名称：`playwright`
6. 在 Command 里输入：`npx -y @anthropic-ai/playwright`
7. 点击保存

保存后，Claude Code 会自动下载安装 Playwright MCP，安装成功后旁边会有绿色圆点。

### 方法二：直接告诉 Claude 安装

你也可以直接对 Claude Code 说：
```
请帮我安装 Playwright MCP
```

然后把下面的命令复制给它：
```
npx -y @anthropic-ai/playwright
```

Claude Code 会自动帮你安装好。

## 常见问题

### Q: MCP 是什么？

MCP = Model Context Protocol，是 Claude Code 的扩展功能。安装 Playwright MCP 后，Claude Code 就能控制你的浏览器进行自动化操作。

### Q: 安装 MCP 需要付费吗？

完全免费！Playwright MCP 是开源免费的。

### Q: 如何找到我的浏览器Profile路径？

**Chrome:**
1. 打开 `C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\`
2. 找到你的Profile文件夹（如 Profile 1、Profile 2）

**Edge:**
1. 打开 `C:\Users\你的用户名\AppData\Local\Microsoft\Edge\User Data\`
2. 找到你的Profile文件夹

### Q: 调试端口是什么？

- Chrome 默认: `9222`
- Edge 默认: `9223`

### Q: 浏览器必须已登录吗？

是的，这个Skill使用本地已登录的浏览器账号，所以你需要：
1. 在浏览器中手动登录你的X(Twitter)账号
2. 使用已登录的Profile

### Q: MCP 安装成功了但不能用？

1. 重启 Claude Code
2. 检查浏览器是否已打开并登录了账号
3. 确保调试端口没有被其他程序占用

## 配置示例

### Chrome 配置示例（Windows）

```bash
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\Profile 1" "https://x.com/你的用户名"
```

### Edge 配置示例（Windows）

```bash
"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --remote-debugging-port=9223 --user-data-dir="C:\Users\你的用户名\AppData\Local\Microsoft\Edge\User Data\Profile 1" "https://x.com/你的用户名"
```

## 注意事项

1. **安全**: 浏览器用户数据包含敏感信息，请勿分享你的用户数据目录
2. **Profile选择**: 确保选择已登录目标账号的浏览器Profile
3. **端口冲突**: 如果端口被占用，可以修改调试端口号
4. **MCP 安装后**: 首次使用需要等待几秒钟让 MCP 启动完成

## 许可证

MIT License

## 更新日志

### v1.0.0
- 初始版本
- 支持X(Twitter)、Gmail等网站自动化
- 可配置你自己的浏览器账号
- 详细 MCP 安装教程
