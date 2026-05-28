# 🌌 Luminos Planner · 蓝境计划

<div align="center">

![Version](https://img.shields.io/badge/version-3.0-blue?style=flat-square&color=1565c0)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square&color=0d2d54)
![Size](https://img.shields.io/badge/size-~140KB-blue?style=flat-square&color=1e88e5)
![Dependencies](https://img.shields.io/badge/backend-Supabase-blue?style=flat-square&color=42a5f5)

**一个面向学生的星空主题学习计划工具**

*云端同步 · 多设备通用 · AI 智能助手 · 零服务器运维*

[🌐 立即体验](https://chocococ0.github.io/Luminous-Planner/) · [功能一览](#-功能一览) · [部署教程](#-自行部署)

</div>

-----

## ✨ 项目亮点

> Luminos 源自拉丁语词根 *lumin-*（光），意为「星辉计划」——
> 用星空美学包裹严肃的学习管理，让每次完成任务都像点亮一颗星。

- 🎨 **深海星空主题** — 精心调配的蓝色渐变 + 动态星点背景
- ☁️ **云端多设备同步** — Supabase 实时同步，手机电脑数据一致
- 📱 **全平台响应式** — 手机、iPad、桌面三档布局自适应
- 🤖 **AI 学习助手** — DeepSeek 驱动，自然语言添加任务/获取鼓励/学习规划
- 🏆 **积分成长体系** — 6 级称号 + 可自定义兑换商店

-----

## 📋 功能一览

### 🗓 三层计划体系（今日 ↔ 本周 ↔ 学期联动）

**今日计划**

- 📌 固定时间任务（锚点，其他任务自动绕行）
- 🔄 循环任务（每天/工作日/每周，自动注入今日列表）
- ⏱ 精确计时器（秒级，超时变红，同时只允许一个任务计时）
- 🧠 智能排程引擎（从当前时刻排列，自动穿插休息，绕开吃饭睡觉时间）
- 📊 可视化时间轴（色块 + 餐饮/睡眠背景层 + 实时光标）
- ☁️ **多设备实时同步**（Supabase Realtime，切换设备数据自动合并）

**本周计划**

- 截止日期 → 自动规划建议完成日 → 推送到今日安排
- 提前完成 +8 积分，**昨日未完成每项扣 3 积分**

**学期课程**

- 以科目为单位，五星自评章节掌握度（了解/熟悉/掌握/精通/大师）
- 积分按等级差值浮动：+1 / +3 / +5 / +8 / +12，降级会扣回
- 学期进度条 + 考试里程碑，设置起始日期后自动推算当前周次
- 考试倒计时 Banner，≤7 天橙色脉冲，≤3 天红色警报

### 🤖 AI 学习助手（DeepSeek）

|功能        |示例             |
|----------|---------------|
|💬 自然语言添加任务|“每天早上8点背单词30分钟”|
|🔄 创建循环任务  |“工作日下午复习线代一小时” |
|🌟 个性化鼓励   |结合今日完成情况生成，非套话 |
|📋 科学规划建议  |基于考试日期和掌握薄弱点   |
|📊 今日复盘    |总结 + 明日建议      |

每日 **50 次**对话额度，次日零点重置。

### ✦ 积分体系

|行为         |积分      |
|-----------|--------|
|✅ 完成今日任务   |+10     |
|⏱ 按时完成     |+5      |
|🔥 连续完成 3 项 |+15     |
|📅 提前完成周任务  |+8      |
|🎯 今日全部完成   |+20     |
|⭐ 章节掌握（按等级）|+1 ~ +12|
|🎓 完成科目     |+20     |
|💤 昨日未完成任务  |**-3/项**|

可自定义兑换商店（奶茶/游戏/追剧…），也可添加自己的奖励项。

### 🏆 全球排行榜

所有账号共享同一排行榜，Supabase 云端实时同步，只记录历史最高分。

-----

## 🔐 账户与数据

- **注册/登录**：Supabase Auth，密码加密存储
- **数据存储**：云端 PostgreSQL + 本地 localStorage 双重备份
- **离线可用**：无网络时自动使用本地缓存，恢复网络后自动同步
- **数据隔离**：Row Level Security 确保每个账号只能访问自己的数据

-----

## 🌐 在线访问

> **<https://chocococ0.github.io/Luminous-Planner/>**

-----

## 🛠 自行部署

### 1. Fork 仓库 & 开启 GitHub Pages

```bash
# Fork 后克隆
git clone https://github.com/你的用户名/Luminous-Planner.git
```

仓库 Settings → Pages → Branch: main → Save

### 2. 创建 Supabase 项目

1. [supabase.com](https://supabase.com) 注册 → New Project
1. SQL Editor → 执行 `supabase_schema.sql` 建表
1. Authentication → Settings → 关闭 **Confirm email**
1. Settings → API → 复制 **Project URL** 和 **anon key**

### 3. 部署 AI 转发函数

```bash
# 安装 Supabase CLI
npm install -g supabase

# 登录并链接项目
supabase login
supabase link --project-ref 你的项目ID

# 设置 DeepSeek Key
supabase secrets set DEEPSEEK_KEY=sk-你的key

# 部署
supabase functions deploy ai-proxy --no-verify-jwt
```

### 4. 填入配置

在 `planner.html` 顶部 `<script>` 块里找到：

```javascript
var SUPA_URL  = 'https://YOUR_PROJECT.supabase.co';
var SUPA_ANON = 'YOUR_ANON_KEY';
var AI_CONFIG = {
  endpoint: 'https://YOUR_PROJECT.supabase.co/functions/v1/ai-proxy',
  ...
};
```

替换后推送到 GitHub，Pages 自动更新。

-----

## 🛠 技术栈

```
前端          HTML5 + 原生 CSS + 原生 JS (ES2020+)  ~140KB 单文件
认证 & 数据   Supabase (PostgreSQL + Auth + Realtime)
AI 转发       Supabase Edge Function (Deno) → DeepSeek API
托管          GitHub Pages
```

-----

## 🔭 未来计划

- [ ] PWA 支持（离线使用 + 添加到主屏幕）
- [ ] 数据导出（JSON / CSV）
- [ ] 微信/邮件考试提醒推送
- [ ] 深色/浅色主题切换

-----

## 📄 License

MIT · 自由使用、修改和分发

-----

<div align="center">

*“每一个完成的任务，都是星图上点亮的一颗星。”*

**⭐ 如果对你有帮助，欢迎 Star**

</div>