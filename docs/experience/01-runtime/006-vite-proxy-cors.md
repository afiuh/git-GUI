---
id: 006
version: 1.0
meta-actions: [M20, I16]
enforce-type: checklist
priority: high
---
## 经验卡片 #006 (Runtime)
- **触发场景：** 前后端分离项目，前端需要调用本地后端 API
- **关联元动作：** [M20 初始化], [I16 通信]
- **问题描述：** 直接使用静态 HTML + JS 会遇到 CORS 问题，后端需要特殊配置
- **解决方案：** 使用 Vite 作为开发服务器，通过 `vite.config.js` 配置代理：
  ```js
  // vite.config.js
  server: {
    proxy: {
      '/api': 'http://localhost:3001'
    }
  }
  ```
- **预防规则：** 前后端分离项目必须使用 Vite/Webpack 等构建工具，避免 CORS 问题
- **端口规范：** 后端 3001，Vite 前端 5173
- **状态：** ✅ 已入库
- **创建日期：** 2026-04-24
- **审核人：** 陈懿灵
