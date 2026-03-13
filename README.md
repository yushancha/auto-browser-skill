# 自动浏览器 Skill

装上后只需要在 Claude Code 进入你所在想进入的浏览器，来浏览、操控你的浏览器，并发消息、查看邮箱。

## 功能特性

- 🤖 自动执行浏览器操作
- 🔍 支持搜索X(Twitter)、Google、百度等平台
- 📧 可以查看和操作邮箱
- 📱 支持各种网页自动化任务
- 🔐 使用本地已登录的浏览器账号
- 💬 可以帮你回复消息

## 前置要求

1. **安装 Claude Code**: [官方下载](https://claude.com/download)
2. **安装 Playwright MCP**: 在 Claude Code 中配置
3. **本地浏览器已登录**: 你需要有一个已登录X(Twitter)或其他网站账号的浏览器

## 安装步骤

### 1. 配置 Playwright MCP

在 Claude Code 的 `settings.json` 中添加：

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/playwright"]
    }
  }
}
```

### 2. 安装 Skills

将 `SKILL.md` 复制到你的 Claude Code skills 目录：

```
Windows: C:\Users\你的用户名\.claude\skills\
Mac/Linux: ~/.claude/skills/
```

### 3. 配置你自己的浏览器账号

打开 `SKILL.md`，找到"浏览器配置信息"部分，修改以下内容：

```bash
# 将这些占位符替换成你自己的信息
<你的Chrome路径>           → 你的Chrome安装路径
<你的用户数据目录>         → 你的浏览器用户数据目录
<你的用户名>              → 你的X用户名
<你的Profile>             → 你的浏览器Profile编号
```

## 使用示例

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开我的X账号" | 打开你配置的X主页 |
| "打开X搜索小互" | 打开X搜索小互并进入主页 |
| "查看今天发的内容" | 进入主页查看最新帖子 |
| "打开邮箱" | 打开Gmail查看最新邮件 |
| "帮我回复这条消息" | 打开消息并回复 |

## 常见问题

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

## 许可证

MIT License

## 更新日志

### v1.0.0
- 初始版本
- 支持X(Twitter)、Gmail等网站自动化
- 可配置你自己的浏览器账号
