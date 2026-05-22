# 私有维护变更日志模板（CHANGELOG_PRIVATE）

> 用途：记录你们团队在开源 v7.0.1 基线上的私有改动，便于追溯、审计和回滚。

## 记录规范

- 日期格式：`YYYY-MM-DD`
- 版本格式：`v7.0.1-custom.<yyyymmdd>.<n>`
- 每条记录至少包含：变更范围、影响评估、回滚方案、验证证据。

## 模板

### [版本号] - YYYY-MM-DD

- **类型**：`feature` / `fix` / `refactor` / `docs` / `hotfix`
- **模块**：如 `Profinet/Siemens`、`ModBus/ModbusTcp`、`Core/Net` 等
- **变更摘要**：
  - 
- **动机 / 问题现象**：
  - 
- **影响范围**：
  - 设备：
  - 协议：
  - 接口行为：
- **兼容性结论**：
  - 
- **回滚方案**：
  - 
- **验证证据**：
  - 对应回归清单：`docs/REGRESSION_CHECKLIST.md`
  - 对应设备矩阵：`docs/DEVICE_MATRIX.md`
  - 日志/抓包链接：

---

## 示例

### [v7.0.1-custom.20260521.1] - 2026-05-21

- **类型**：fix
- **模块**：`ModBus/ModbusTcp`
- **变更摘要**：
  - 调整超时后重试逻辑，超时时仅重试一次。
- **动机 / 问题现象**：
  - 部分现场在网络抖动时批量读寄存器失败率偏高。
- **影响范围**：
  - 设备：通用 Modbus TCP 从站
  - 协议：Modbus TCP
  - 接口行为：失败请求增加一次自动重试
- **兼容性结论**：
  - 旧接口签名不变，行为向后兼容。
- **回滚方案**：
  - 回退至标签 `v7.0.1-custom.20260520.3`。
- **验证证据**：
  - 对应回归清单：`docs/REGRESSION_CHECKLIST.md`
  - 对应设备矩阵：`docs/DEVICE_MATRIX.md`
  - 日志/抓包链接：内部文档链接
