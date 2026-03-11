# OpenClaw 实践案例集

本仓库收集了 OpenClaw 的真实应用案例和使用示例，帮助您快速了解如何使用 OpenClaw 解决实际问题。

## 📚 目录

- [开发工具](#开发工具)
- [自动化工作流](#自动化工作流)
- [知识管理](#知识管理)
- [语音与电话](#语音与电话)
- [基础设施](#基础设施)
- [家庭与硬件](#家庭与硬件)
- [社区项目](#社区项目)

---

## 🛠️ 开发工具

### PR Review 自动化
**作者:** @bangnokia
**功能:** 代码变更完成后自动创建 PR，OpenClaw 审查代码差异并通过 Telegram 反馈建议和合并决策

```bash
# 示例配置
# 1. 配置 GitHub Webhook
openclaw webhook configure --type github --repo owner/repo

# 2. 配置 Telegram 通知
openclaw channel connect telegram

# 3. 发送消息让 OpenClaw 审查 PR
"请审查 https://github.com/owner/repo/pull/123"
```

**使用场景:**
- 代码审查自动化
- CI/CD 流程集成
- 团队协作通知

### SNAG - 截图转 Markdown
**作者:** @am-will
**项目:** https://github.com/am-will/snag
**功能:** 热键选择屏幕区域 → Gemini 视觉识别 → 自动转换 Markdown 并复制到剪贴板

```bash
# 安装和配置
git clone https://github.com/am-will/snag.git
cd snag
npm install

# 配置 OpenClaw 技能
mkdir -p ~/.openclaw/workspace/skills/snag
cp SKILL.md ~/.openclaw/workspace/skills/snag/

# 使用
# 1. 按下热键选择屏幕区域
# 2. 自动生成 Markdown
# 3. 内容已在剪贴板中
```

**使用场景:**
- 快速文档编写
- UI 设计评审
- bug 报告截图

### CodexMonitor
**作者:** @odrobnik
**项目:** https://clawhub.com/odrobnik/codexmonitor
**功能:** 监控本地 OpenAI Codex 会话（CLI 和 VS Code），列出、检查和监视会话状态

```bash
# 安装
clawhub install codexmonitor

# 使用示例
codex list                    # 列出所有 Codex 会话
codex inspect <session-id>    # 检查会话详情
codex watch                   # 实时监控会话

# 与 OpenClaw 集成
"检查我当前运行的 Codex 会话"
"监控 Codex token 使用情况"
```

**使用场景:**
- 开发会话管理
- Token 使用监控
- 调试和分析

### Linear CLI
**作者:** @NessZerra
**项目:** https://github.com/Finesssee/linear-cli
**功能:** Linear 命令行工具，与 Claude Code 和 OpenClaw 的 AI 工作流集成

```bash
# 安装
npm install -g @finesssee/linear-cli

# 配置 Linear API Key
linear auth login

# 使用示例
linear issue list                    # 列出所有 issues
linear issue create "Bug in login"   # 创建 issue
linear project list                  # 列出项目

# 与 OpenClaw 集成
"列出 Linear 上所有高优先级 bugs"
"在 Linear 创建新 issue：首页加载失败"
```

**使用场景:**
- 项目管理自动化
- Issue 跟踪
- 开发流程集成

---

## 🤖 自动化工作流

### 研报因子挖掘
**作者:** @supersush
**功能:** 自动从券商研报中提取投资因子（如财务指标、估值指标、技术指标等），智能分析因子有效性并生成结构化因子库

![研报因子挖掘演示](images/research-factor-mining.jpg)

```bash
# 配置研究技能
skillhub install akshare-stock

# 使用示例
"分析这份研报的选股因子"
"提取研报中的财务指标和估值方法"
"生成因子有效性分析报告"

# 输出结果
✅ 因子清单：提取的指标及定义
✅ 因子分析：有效性评估和回测建议
✅ 结构化数据：JSON/CSV格式的因子库
```

**因子类型:**
- 财务指标因子（ROE、毛利率、现金流等）
- 估值指标因子（PE、PB、PS等）
- 技术指标因子（动量、波动率、成交量等）
- 事件驱动因子（增减持、业绩预告等）

**使用场景:**
- 量化投资策略开发
- 研报信息结构化提取
- 因子库构建与维护
- 投资研究自动化

---

### Tesco 购物自动化
**作者:** @marchattonhere
**功能:** 每周膳食计划 → 常规商品 → 预订配送时段 → 确认订单，完全通过浏览器控制实现

```bash
# 配置浏览器自动化
# 1. 安装 OpenClaw browser 工具
openclaw browser enable

# 2. 创建购物脚本
mkdir -p ~/.openclaw/workspace/skills/tesco-shop
cat > ~/.openclaw/workspace/skills/tesco-shop/SKILL.md << 'EOF'
# Tesco 购物自动化

使用 browser 工具自动化 Tesco 在线购物流程。

## 流程
1. 登录 Tesco 账户
2. 从膳食计划生成购物清单
3. 添加常规商品
4. 选择配送时段
5. 确认订单

## 触发方式
用户说："开始每周购物" 或 "预订下周配送"
EOF

# 3. 使用
"开始每周购物"
"预订下周二下午的配送"
```

**使用场景:**
- 定期购物自动化
- 生活事务简化
- 浏览器自动化学习

### ParentPay 学童餐预订
**作者:** @George5562
**功能:** 自动化英国学校餐费预订，使用鼠标坐标精确点击表格单元格

```bash
# 安装技能
clawhub install parentpay-automation

# 配置登录信息和儿童信息
openclaw config set parentpay.username "your@email.com"
openclaw config set parentpay.password "password"
openclaw config set parentpay.child_name "Child Name"

# 使用
"预订下周的学校午餐"
"查看本月的餐费预订情况"
```

**使用场景:**
- 重复性表单填写
- 教育相关事务自动化
- 浏览器自动化实践

### R2 文件上传 (Send Me My Files)
**作者:** @julianengel
**项目:** https://clawhub.com/skills/r2-upload
**功能:** 上传文件到 Cloudflare R2/S3 并生成安全的预签名下载链接

```bash
# 安装
clawhub install r2-upload

# 配置 R2 凭证
openclaw config set r2.account_id "your_account_id"
openclaw config set r2.access_key "your_access_key"
openclaw config set r2.secret_key "your_secret_key"
openclaw config set r2.bucket "my-bucket"

# 使用
"上传 screenshot.png 到 R2"
"分享文件 document.pdf 给我"
```

**使用场景:**
- 远程 OpenClaw 实例的文件共享
- 临时文件分享
- 云存储集成

### Beeper CLI
**作者:** @jules
**项目:** https://github.com/blqke/beepcli
**功能:** 通过 Beeper Desktop 本地 MCP API 读取、发送和归档消息，统一管理 iMessage、WhatsApp 等所有聊天

```bash
# 安装
npm install -g beepcli

# 配置 Beeper Desktop MCP
beepcli configure

# 使用示例
beepcli list                   # 列出所有对话
beepcli send --chat "+123456" "Hello from OpenClaw"
beepcli archive --chat "+123456"

# 与 OpenClaw 集成
"通过 Beeper 发送消息给 Mom"
"检查 iMessage 未读消息"
"归档所有已处理的 WhatsApp 对话"
```

**使用场景:**
- 多平台消息统一管理
- 自动化消息归档
- 跨平台消息同步

---

## 🧠 知识管理

### Wine Cellar Skill
**作者:** @prades_maxime
**功能:** 从 CSV 导入酒窖数据，快速构建本地酒窖管理技能（示例：962 瓶酒）

```bash
# 1. 准备 CSV 数据文件
cat > /tmp/wine-cellar.csv << 'EOF'
name,vintage,region,variety,rating
Château Margaux,2015,Bordeaux,Red,98
Dom Pérignon,2012,Champagne,Sparkling,95
EOF

# 2. 让 OpenClaw 创建技能
"我需要一个酒窖管理技能，数据在 /tmp/wine-cellar.csv"
"请将这些酒存储在 ~/.openclaw/wine-cellar/"

# 3. 使用技能
"我有多少瓶 2015 年的红酒？"
"推荐一瓶评分超过 95 的香槟"
"按产区列出我的酒窖库存"
```

**使用场景:**
- 个人收藏管理
- 自定义技能开发学习
- 数据库查询自动化

### Oura Ring 健康助手
**作者:** @AS
**功能:** 整合 Oura Ring 数据与日历、预约和健身计划的个人 AI 健康助手

```bash
# 安装依赖技能
clawhub install oura-ring

# 配置 Oura API
openclaw config set oura.access_token "your_token"

# 连接日历
openclaw channel connect google

# 使用
"根据我的睡眠质量安排今天的任务"
"查看本周的恢复分数趋势"
"提醒我在体力不足时调整健身计划"
"生成健康周报"
```

**使用场景:**
- 健康数据可视化
- 智能日程安排
- 个人健康分析

---

## 🎙️ 语音与电话

### Telegram 语音笔记 (papla.media)
**作者:** Community
**项目:** https://papla.media/docs
**功能:** 封装 papla.media TTS 服务，将结果作为 Telegram 语音笔记发送（无自动播放烦恼）

```bash
# 1. 配置 papla.media API
openclaw config set papla.api_key "your_api_key"

# 2. 安装技能
mkdir -p ~/.openclaw/workspace/skills/papla-tts
cat > ~/.openclaw/workspace/skills/papla-tts/SKILL.md << 'EOF'
# Telegram 语音笔记 TTS

使用 papla.media 将文本转换为 Telegram 语音笔记。

## 配置
- papla.api_key: papla.media API 密钥

## 使用
用户说："用语音发送..." 或 "语音告诉我..."
EOF

# 3. 使用
"用语音告诉我明天的天气预报"
"语音总结这篇文章：https://example.com/article"
```

**使用场景:**
- 语音消息播报
- 内容音频化
- 无障碍访问

---

## 🏗️ 基础设施

### Kev's Dream Team (14+ Agents)
**作者:** @adam91holt
**项目:** https://github.com/adam91holt/orchestrated-ai-articles
**功能:** 14+ 个 agent 在一个 gateway 下，Opus 4.5 编排器委派给 Codex workers

```bash
# 克隆配置仓库
git clone https://github.com/adam91holt/clawdspace.git
cd clawdspace

# 安装配置
cp config/openclaw.json ~/.openclaw/openclaw.json

# 查看架构
cat ARCHITECTURE.md

# 启动多 agent 系统
openclaw gateway start

# agent 通信
"让 research agent 搜索最新的 AI 新闻"
"让 coding agent 实现这个功能"
"让 review agent 审查代码"
```

**使用场景:**
- 多 agent 协作
- 任务自动化分发
- 复杂系统管理

---

## 🏠 家庭与硬件

### Bambu 3D 打印机控制
**作者:** @tobiasbischoff
**项目:** https://clawhub.com/tobiasbischoff/bambu-cli
**功能:** 控制和故障排除 BambuLab 打印机：状态、任务、摄像头、AMS、校准等

```bash
# 安装技能
clawhub install bambu-cli

# 配置打印机 IP
openclaw config set bambu.printer_ip "192.168.1.100"
openclaw config set bambu.access_code "your_access_code"

# 使用
"检查 3D 打印机状态"
"查看当前打印进度"
"拍摄打印舱照片"
"更换 AMS 材料"
"开始打印 test.gcode"
```

**使用场景:**
- 远程 3D 打印管理
- 制造自动化
- IoT 设备集成

### Vienna 交通 (Wiener Linien)
**作者:** @hjanuschka
**项目:** https://clawhub.com/hjanuschka/wienerlinien
**功能:** 维也纳公共交通实时出发、故障、电梯状态和路线规划

```bash
# 安装技能
clawhub install wienerlinien

# 使用
"下一班地铁到 Stephansplatz 什么时候？"
"有交通延误吗？"
"规划到 Oper 的路线"
"检查 59A 路电梯状态"
```

**使用场景:**
- 通勤助手
- 实时交通信息
- 城市服务集成

---

## 🎯 快速开始

### 1. 安装 OpenClaw

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
```

### 2. 配置频道

```bash
# 连接 Telegram
openclaw channel connect telegram

# 或连接 WhatsApp
openclaw channel connect whatsapp
```

### 3. 安装技能

```bash
# 从 ClawHub 安装
clawhub install <skill-name>

# 或手动安装
mkdir -p ~/.openclaw/workspace/skills/my-skill
# 将 SKILL.md 放入该目录
```

### 4. 开始使用

向您的 OpenClaw 发送消息开始对话！

---

## 📖 学习资源

### 视频教程

- **OpenClaw 完整设置教程** (28分钟) - VelvetShark
  - [第1部分](https://www.youtube.com/watch?v=SaWSPZoPX34)
  - [第2部分](https://www.youtube.com/watch?v=mMSKQvlmFuQ)
  - [第3部分](https://www.youtube.com/watch?v=5kkIJNUGFho)

### 官方文档

- [OpenClaw 官网](https://openclaw.ai/)
- [文档](https://docs.openclaw.ai/)
- [入门指南](https://docs.openclaw.ai/start/getting-started)
- [Showcase](https://docs.openclaw.ai/start/showcase)

### 社区

- [Discord](https://discord.gg/clawd)
- [GitHub Discussions](https://github.com/openclaw/openclaw/discussions)
- [ClawHub](https://clawhub.com/) - 技能注册中心

---

## 🤝 贡献

欢迎提交您的 OpenClaw 使用案例！

1. Fork 本仓库
2. 创建新文件或修改现有内容
3. 提交 Pull Request

---

## 📝 许可证

MIT License

---

## 🔗 相关链接

- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [ClawHub 技能市场](https://clawhub.com/)
- [社区 Discord](https://discord.gg/clawd)

---

**Happy Building! 🦞**

*本仓库持续更新中，欢迎分享您的 OpenClaw 实践经验！*
