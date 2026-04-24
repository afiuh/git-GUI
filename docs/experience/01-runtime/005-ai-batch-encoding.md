---
id: 005
version: 1.0
meta-actions: [P10, M15]
enforce-type: checklist
priority: high
---
## 经验卡片 #005 (Seed)
- **触发场景：** AI 生成 .bat 批处理文件，运行时报中文乱码
- **关联元动作：** [P10 编码规范], [M15 文件生成]
- **问题描述：** 批处理文件中中文字符显示为乱码，如"成功"显示为"�ɹ�"
- **根本原因：** AI 默认生成 UTF-8 编码文件，而 Windows cmd 默认使用 GBK/ANSI 编码读取
- **解决方案：**
  1. **生成时指定编码**：要求 AI 生成文件时注明"必须使用 GBK/ANSI 编码"
  2. **手动转换编码**：
     ```powershell
     # PowerShell 转换
     Get-Content -Path "file.bat" -Encoding UTF8 | Out-File -FilePath "output.bat" -Encoding Default
     ```
  3. **记事本另存为**：打开 bat → 另存为 → 编码选择 ANSI
  4. **使用 .ps1 替代**：PowerShell 默认支持 UTF-8，长脚本优先用 .ps1
- **预防规则：** 生成 Windows 脚本时，优先指定编码或生成 .ps1 文件
- **工具链映射：** -
- **状态：** ✅ 已入库
- **创建日期：** 2026-04-24
- **审核人：** -
