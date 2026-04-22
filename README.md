# EP Cross Promote · Web Mockup

PRD [prd_ep_cross_promote.md](../PRD/prd_ep_cross_promote.md) 的可交互 mockup，用于和其他 PM / 设计 / 开发对齐视觉效果和文案方案。

## 快速预览

```bash
# 方式一：直接打开
open index.html

# 方式二：本地起 server（如果浏览器打不开 CDN 资源）
python3 -m http.server 8000
# 然后访问 http://localhost:8000/index.html
```

## 页面结构

- **背景**：简化版 AIO Web GUI（sidebar + Welcome + Jump Back In + All Study Sets），参考 [aio26.vercel.app](https://aio26.vercel.app)
- **Banner**：底部固定 Banner（方案 A）
- **Popup**：整屏遮罩 + 中央 EP Onboarding 弹窗（方案 B），复刻 [Figma node 5728-157443](https://www.figma.com/design/wCdwhJnDpW8ijtX0AbML9h/26.1-2-3-4-WebAIO---%E8%BF%AD%E4%BB%A3?node-id=5728-157443)
- **调试面板**：右上角浮动面板，切换触发源 + 方案组合

## 调试面板使用

| 区域 | 选项 | 说明 |
|-----|------|-----|
| 触发源 | Paywall Close / Stripe Fail / Sub Fail / Cover Idle 5s | 前 3 个立即展示；Cover Idle 有 5 秒倒计时 |
| Banner 方案 | Off / A1 / A2 / A3 | ★ A1 推荐 |
| Popup 方案 | Off / B1 / B2 / B3 | ★ B1 推荐 |
| 快速组合 | A1+B1 / A2+B2 / A3+B3 | 一键切换整套方案组合 |

## 文案方案索引（与 PRD 完全一致）

### Banner（方案 A）

| ID | 主文案 | 主 CTA |
|----|-------|-------|
| **A1 · 诚实试用型（推荐）** | Ready for your exam? Get a free preview of what's likely on your Final with Exam Predictor. | `Try Exam Predictor` |
| A2 · 量化免费范围 | Worried about your Final? Generate your first Mock Exam free — see AI-predicted questions before you study. | `Generate My First Mock` |
| A3 · 价值 + 社交证明 | Don't study blind. 75% of students said Exam Predictor matched their real Final — try your first mock on us. | `Try My First Mock` |

Banner 次要操作（所有方案一致）：
- `Dismiss`（文字链）：本次关闭，下次触发仍会展示
- `Don't show again`（灰色小字）：永久关闭

### Popup（方案 B）

| ID | 主标题 | 主 CTA |
|----|-------|-------|
| **B1 · 诚实首次免费（推荐）** | 🚀 Walk Into Your Exam 100% Ready | `Try My First Mock Free` |
| B2 · 痛点 + 明确边界 | Don't leave empty-handed — 🚀 Walk Into Your Exam 100% Ready | `Preview My Mock Exam` |
| B3 · 最低承诺 + 紧迫感 | Your Final is coming. Start with a free sample. | `Try a Free Sample` |

副标题和右侧 3 点价值保持 EP Onboarding 原文案不变。

Popup 次要操作：
- `Maybe Later` / 点击遮罩 / 右上角 X：本次关闭
- `Don't show again`（灰色小字）：永久关闭

## 交互行为

| 动作 | 效果 |
|-----|-----|
| 点主 CTA | Toast 提示"跳转 EP 创建流程"，Popup/Banner 关闭 |
| 点 Banner `Dismiss` | 关闭 Banner，Toast 本次关闭 |
| 点 Banner `Don't show again` | 关闭 Banner，Toast 永久关闭（对应 user property 写入） |
| 点 Popup `Maybe Later` / 遮罩 / X | 关闭 Popup，Toast 本次关闭 |
| 点 Popup `Don't show again` | 关闭 Popup，Toast 永久关闭 |
| 切 Cover Idle 5s | 5 秒倒计时后展示 |

## 对应 PRD 章节

| Mockup 元素 | PRD 章节 |
|------------|---------|
| 触发源（4 类） | [触发条件](../PRD/prd_ep_cross_promote.md) / 展示时机 |
| Cover Idle 5s | [cover_idle_timing/findings.md](../cover_idle_timing/findings.md) 数据支撑 |
| Banner A1/A2/A3 | 方案 A 对比表 |
| Popup B1/B2/B3 | 方案 B 对比表 |
| Don't show again | 展示频率逻辑（`ep_guide_dismissed_permanent` user property） |

## 已知局限

- 仅桌面端 1280-1440 宽度优化，未做响应式
- 不包含真实埋点上报，交互仅为可视化演示
- 背景为简化版 AIO GUI 复刻，非像素级精度
- 无构建流程，所有资源通过 Tailwind CDN 和纯 JS 实现；无网络时 CDN 不可用

## 文件清单

```
cross_promote_mockup/
├── index.html      # 单文件 mockup（HTML + CSS + JS）
└── README.md       # 本文件
```
