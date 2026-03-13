# 自动浏览网页 Skill

## 功能

使用 Playwright MCP 控制浏览器，自动搜索、浏览网页、提取内容。

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
| "搜索xxx" | 先打开 Google，搜索 xxx |

### 进阶规则

当用户说"打开谷歌浏览器并..."时：

1. **解析用户完整意图**
   - 用户说"打开谷歌浏览器并在x搜索小互并进入他的主页"
   - → 自动打开 x.com → 搜索"小互" → 进入主页

2. **具体账号访问**
   - 用户说"打开我的X账号"或类似指令
   - → 打开你配置的X主页

3. **灵活处理**
   - 根据用户提到的平台（Google、X/Twitter、百度等）自动选择
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

**第一步：启动本地浏览器（已登录你的X账号）**

用户说"打开我的X账号"或类似指令时，启动你本地已登录的浏览器：

```bash
# Chrome 启动命令
"<你的Chrome路径>" --remote-debugging-port=9222 --user-data-dir="<你的用户数据目录>" "https://x.com/<你的用户名>"

# 示例（Windows）
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\Profile 1" "https://x.com/你的用户名"
```

**第二步：用Playwright连接并操作**

用 `browser_navigate` 打开目标页面后，可以执行各种任务：

| 用户指令 | 执行操作 |
|---------|---------|
| "打开X搜索xxx" | 打开 x.com → 搜索xxx → 进入主页 |
| "查看今天发了什么" | 进入主页 → 找到最新帖子 → 提取内容 |
| "打开邮箱" | 打开邮箱网站（如 Gmail）→ 查看最新邮件 |
| "回复邮件" | 打开邮件 → 阅读内容 → 回复 |
| "执行邮件里的任务" | 打开邮件 → 提取任务 → 执行 |

### 核心原则

1. **打开浏览器后自动进入你配置的X主页**
2. **只要进入你的账号后，可以执行任何任务**：X搜索、邮箱、浏览网页等
3. **无需询问用户确认**，直接执行

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
   - `<你的用户名>` → 你的X用户名
   - `<你的Profile>` → 你的浏览器Profile编号

2. 查看你的Profile路径：
   - Chrome: `C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\`
   - Edge: `C:\Users\你的用户名\AppData\Local\Microsoft\Edge\User Data\`

3. 选择你已登录X账号的Profile编号（如 Profile 1、Profile 2 等）
