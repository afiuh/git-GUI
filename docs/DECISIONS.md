# 技术决策记录

## 项目名称
Git GUI - 面向开发者的 Web Git 客户端

## 后端框架选择：Express.js
- 依据：需求文档 §6.1 明确指定 "Node.js + Express + simple-git"
- 备选：Fastify，性能更好但需求文档未指定
- 创建日期：2026-04-24

## 前端框架选择：Vite + 原生 JavaScript
- 依据：使用 Vite 开发服务器，避免 CORS 问题，简化开发体验
- 技术栈：原生 JS（简化复杂度，不用 React）
- Vite 端口：5173（开发），代理 `/api/*` 到 backend:3001
- 创建日期：2026-04-24

## 超时机制
- Git 命令执行超时时间：60 秒
- 超时后返回错误提示

## 持久化策略
- `localStorage.lastRepoPath`：最近打开的仓库路径
- `localStorage.theme`：主题偏好（light | dark）
- `localStorage.pipelines`：流水线配置（JSON 数组）

## 目录结构
```
git-GUI/
├── backend/                    # 后端 API 服务
│   ├── server.js              # [M20 初始化] Express 入口，端口 3001
│   ├── config.js              # [I15 存储] 配置
│   ├── routes/
│   │   └── git.js             # [I14 用户输入] Git API 路由
│   ├── services/
│   │   └── gitService.js      # [M5 转换] simple-git 封装
│   └── utils/
│       └── errors.js          # [F12 捕获] 异常处理
├── frontend/                   # 前端（Vite 项目）
│   ├── package.json           # 前端依赖
│   ├── vite.config.js         # Vite 配置，代理 /api 到 backend
│   ├── index.html              # 入口 HTML
│   ├── css/
│   │   └── style.css           # 样式（含主题变量）
│   └── js/
│       ├── main.js             # [M20 初始化] 入口
│       ├── api.js              # [I16 通信] API 调用封装
│       ├── app.js              # [M5 转换] 主应用逻辑
│       └── components/         # UI 组件
│           ├── BranchPanel.js  # 左侧栏：分支管理
│           ├── ChangePanel.js  # 中间栏：变更管理
│           ├── HistoryPanel.js # 右侧栏：快照管理
│           ├── CloneWizard.js  # 克隆向导弹窗
│           ├── PipelinePanel.js # 流水线面板
│           └── Toast.js        # 提示组件
├── start.bat                   # 启动脚本
└── package.json                # 后端依赖
```

**文件数：17 个（新增 PipelinePanel.js）**

## API 响应格式
- 统一遵循：`{ code: 0, message: "success", data: null }`
- code: 0 = 成功，非 0 = 错误

## 经验卡片编号
- Git GUI 项目专用编号段：006+
