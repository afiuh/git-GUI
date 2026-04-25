---
id: 007
version: 1.0
meta-actions: [M5, I14, F12]
enforce-type: checklist
priority: medium
---
## 经验卡片 #007 (Runtime)
- **触发场景：** 需要顺序执行多个 Git 命令（如 status → add → commit → push）
- **关联元动作：** [M5 转换], [I14 用户输入], [F12 捕获]
- **问题描述：** 每次提交推送需要多个步骤，希望一键自动化执行
- **解决方案：** 设计流水线（Pipeline）功能：
  - 每条流水线包含多个步骤
  - 每步定义命令类型和参数
  - 按顺序执行，前一步失败则停止
  - 支持拖拽排序、启用/禁用单个步骤
- **持久化**：使用 `localStorage.pipelines` 存储配置
- **状态：** ✅ 已入库
- **创建日期：** 2026-04-25
- **审核人：** 陈懿灵
