# 自动浏览器 Skill

## 功能

使用 Playwright MCP 控制浏览器，自动搜索、浏览网页、提取内容、发笔记、回复消息等。

## 核心原则

**自动执行，无需确认**
- 用户说完指令后，立即自动调用 MCP 执行
- 不询问用户是否确认，直接行动

---

## 打开浏览器的正确方式

### 默认规则

| 用户指令 | 打开内容 |
|---------|---------|
| "打开谷歌浏览器" | Google 搜索页面（https://www.google.com） |
| "打开百度" | 百度搜索页面（https://www.baidu.com） |
| "打开X" 或 "打开x" | Twitter 搜索页面（https://x.com/explore） |
| "打开我的X账号" | 你的 Twitter 主页 |
| "打开小红书" | 小红书网页版（https://www.xiaohongshu.com） |
| "打开咸鱼" | 闲鱼网页版（https://2.taobao.com） |
| "搜索xxx" | 先打开 Google，搜索 xxx |

### 进阶规则

当用户说"打开谷歌浏览器并..."时：

1. **解析用户完整意图**
   - 用户说"打开X搜索归藏并进入他的主页"
   - → 自动打开 x.com → 搜索"归藏" → 进入主页

2. **具体账号访问**
   - 用户说"打开我的X账号"或类似指令
   - → 打开你配置的X主页

3. **灵活处理**
   - 根据用户提到的平台（Google、X/Twitter、小红书、咸鱼、百度等）自动选择
   - 根据用户提到的账号名自动构建 URL

---

## 执行流程

```
用户指令 → 解析意图 → 自动调用 MCP → 执行操作
```

### MCP 调用顺序

1. `browser_install` - 确保浏览器已安装（如需要）
2. `browser_navigate` - 打开目标网站
3. 根据需要调用其他 MCP：
   - `browser_type` - 输入搜索内容
   - `browser_click` - 点击按钮/链接
   - `browser_snapshot` - 获取页面状态
   - `browser_take_screenshot` - 截图

---

## 记住这个规则

1. **用户说"打开谷歌浏览器" → 打开 Google 搜索页面**
2. **用户说"打开X" → 打开 Twitter/X 搜索**
3. **用户提到"我的账号" → 自动打开配置的X主页**
4. **用户说"搜索xxx" → 自动搜索**
5. **所有操作自动执行，无需询问确认**

---

## ⚠️ 关键规则：使用本地已登录的浏览器

### 完整操作流程

**第一步：启动本地浏览器（已登录你的账号）**

用户说"打开我的X账号"或类似指令时，启动你本地已登录的浏览器：

```bash
# Chrome 启动命令
"<你的Chrome路径>" --remote-debugging-port=9222 --user-data-dir="<你的用户数据目录>" "https://x.com/<你的用户名>"

# 示例（Windows）
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\Profile 1" "https://x.com/你的用户名"
```

**第二步：用Playwright连接并操作**

用 `browser_navigate` 打开目标页面后，可以执行各种任务

---

## 使用示例

### X (Twitter) 相关

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开我的X账号" | 打开你配置的X主页 |
| "打开X搜索归藏" | 打开X搜索归藏 |
| "进入归藏主页" | 进入归藏的主页查看他今天发的内容 |
| "查看今天发了什么" | 进入主页 → 找到最新帖子 → 提取内容 |
| "帮我发一条X笔记" | 打开发帖子界面 → 输入内容 → 发布 |
| "帮我回复这条消息" | 打开消息 → 阅读内容 → 回复 |

### 小红书相关 - 详细操作流程

**发小红书笔记**：
1. 打开小红书网页版：`https://www.xiaohongshu.com`
2. 点击发布笔记按钮
3. 上传图片/视频
4. 输入标题和正文内容
5. 添加话题标签
6. 点击发布

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开小红书" | 打开小红书网页版 https://www.xiaohongshu.com |
| "帮我发小红书笔记" | 打开发布笔记界面 → 上传图片 → 输入标题和正文 → 添加话题 → 发布 |
| "查看小红书消息" | 打开消息中心 → 查看评论、点赞、粉丝等消息 |
| "帮我回复小红书评论" | 打开笔记 → 找到评论 → 输入回复内容 → 发送 |
| "查看我的小红书主页" | 进入你的个人主页 → 查看已发布的笔记 |

### 咸鱼相关 - 详细操作流程

**回复买家消息**：
1. 打开咸鱼网页版：`https://2.taobao.com`
2. 点击消息中心
3. 找到未回复的买家咨询
4. 阅读买家问题
5. 输入回复内容
6. 发送回复

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开咸鱼" | 打开咸鱼网页版 https://2.taobao.com |
| "帮我回复买家消息" | 打开消息中心 → 找到买家咨询 → 阅读问题 → 输入回复 → 发送 |
| "查看今天的新订单" | 进入订单页面 → 查看新订单 → 提取订单信息 |
| "查看咸鱼消息" | 打开消息中心 → 查看所有买家咨询 |
| "帮我上架商品" | 点击发布商品 → 填写商品信息 → 上传图片 → 设置价格 → 发布 |
| "查看我的咸鱼主页" | 进入你的咸鱼店铺主页 |

### 邮箱相关

| 你对Claude说 | Claude会执行 |
|-------------|-------------|
| "打开邮箱" | 打开Gmail或其他邮箱 |
| "查看最新邮件" | 查看收件箱最新邮件 |
| "回复这封邮件" | 打开邮件 → 阅读内容 → 回复 |

---

## 24小时自动回复（进阶功能）

如果想要24小时自动回复消息，需要写一个自动回复脚本：

1. **告诉 Claude Code**：请帮我写一个自动回复脚本

2. **Claude 会根据你的需求创建脚本**，例如：
   - 自动回复 X 粉丝消息
   - 自动回复咸鱼买家咨询
   - 自动回复小红书评论

3. **运行脚本**：让脚本在后台运行，保持浏览器在线即可

### 示例：X自动回复脚本思路

```
1. 每隔1分钟检查一次新消息
2. 如果有新消息，读取消息内容
3. 根据消息内容生成回复
4. 自动发送回复
```

你可以直接告诉 Claude："帮我写一个自动回复X消息的脚本"，它会用自然语言和你对话，了解你的需求后帮你创建。

---

## 浏览器配置信息（需要你修改）

### Chrome

- **浏览器路径**: `C:\Program Files\Google\Chrome\Application\chrome.exe`
- **用户数据目录**: `C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\你的Profile`
- **启动命令**:
  ```bash
  "C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\Profile 1" "https://x.com/你的用户名"
  ```

### Edge

- **浏览器路径**: `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe`
- **用户数据目录**: `C:\Users\你的用户名\AppData\Local\Microsoft\Edge\User Data\你的Profile`
- **启动命令**:
  ```bash
  "C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --remote-debugging-port=9223 --user-data-dir="C:\Users\你的用户名\AppData\Local\Microsoft\Edge\User Data\Profile 1" "https://x.com/你的用户名"
  ```

---

## 如何修改成你自己的账号

1. 找到浏览器启动命令中的以下部分并替换：
   - `<你的Chrome/Edge路径>` → 你的浏览器安装路径
   - `<你的用户数据目录>` → 你的浏览器用户数据目录
   - `<你的用户名>` → 你的X/小红书/咸鱼用户名
   - `<你的Profile>` → 你的浏览器Profile编号

2. 查看你的Profile路径：
   - Chrome: `C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\`
   - Edge: `C:\Users\你的用户名\AppData\Local\Microsoft\Edge\User Data\`

3. 选择你已登录目标账号的浏览器Profile编号（如 Profile 1、Profile 2 等）
