# HslCommunication 开源版（v7.0.1）架构与组成说明

> 本文面向“在免费开源最后版本基础上持续自维护”的使用场景，帮助你快速定位代码与工程边界。

## 1. 仓库定位

本仓库是一个多工程解决方案，包含：

- 多目标框架类库实现（.NET 3.5 / .NET 4.5 / .NET Standard）。
- 若干演示与测试工程（协议示例、服务端示例、UI Demo）。
- 协议说明文档与部分专题文档。

## 2. 解决方案工程组成

`HslCommunication.sln` 主要可分为 3 层：

### 2.1 核心类库层

- `HslCommunication_Net35`：历史兼容版本，适配旧项目。
- `HslCommunication_Net45`：功能最完整的 .NET Framework 主实现。
- `HslCommunication_NetStandard`：跨平台方向实现（供 .NET Core / .NET 5+ 使用）。

### 2.2 测试与示例层

- `HslCommunication_Net45.Test`：Net45 下的测试工程。
- `TestProject/*`：按通信类型拆分的示例（SimplifyNet、FileNet、UdpNet、PushNet、ComplexNet、Demo 等）。
- `HslCommunicationCppDemo`：C++ 调用示例。

### 2.3 工具与配套层

- `软件自动更新`：自动更新相关示例/工具工程。
- `docs/*`：协议文档与说明文档。

## 3. 核心代码目录（以 Net45 为主）

`HslCommunication_Net45` 的目录组织可理解为“通信核心 + 协议实现 + 基础能力 + 可视化与工具”：

- `Core/`：通信抽象、结果模型、网络基类、会话与打包等核心能力。
- `Serial/`：串口通信基础封装。
- `Enthernet/`：网络通信组件（TCP/UDP、文件传输、复杂网络模型、Redis、推送网络等）。
- `Profinet/`：工业协议与厂商驱动（Siemens、Melsec、Omron、AB、LSIS、Panasonic 等）。
- `ModBus/`：Modbus TCP/RTU/ASCII 及相关监控模型。
- `Robot/`：工业机器人通信封装（如 KUKA、YASKAWA、EFORT）。
- `LogNet/`：日志框架与日志查看控件。
- `BasicFramework/`：缓存、加密、邮件、数值处理、授权等工具能力。
- `Algorithms/`：报警、连接池、傅里叶等算法模块。
- `Controls/`：WinForms 可视化控件（仪表、曲线、指示灯等）。
- `Instrument/`：仪器设备相关封装。

## 4. 推荐阅读与二次开发路径

如果你计划在该开源版本上长期维护，建议按以下顺序：

1. **先跑通 Demo**：从 `TestProject/HslCommunicationDemo`、`HslCommunicationCoreDemo` 入手，确认基础环境。
2. **确定主线框架**：
   - 仅 Windows + 历史系统：优先 Net45。
   - 新项目跨平台：优先 NetStandard。
3. **按协议纵向阅读**：例如先看 `Profinet/Siemens` 或 `ModBus/ModbusTcp`，再回到 `Core` 理解通用机制。
4. **建立你自己的“设备回归清单”**：按设备型号、地址区、读写类型（位/字/浮点/字符串）做最小闭环测试。

## 5. 维护建议（开源冻结版本场景）

- **建议冻结上游 API 面**：新增功能尽量通过扩展类或适配层实现，减少对原核心类的侵入。
- **建议建立私有变更日志**：记录每次协议行为变更、异常码调整、超时策略修改。
- **建议补全自动化验证**：至少覆盖你实际使用的 PLC/设备协议组合。
- **建议分层封装业务调用**：业务系统只依赖你自己的二次封装，不直接散落调用底层协议类。

## 6. 文档索引

- 总览：`README.md`
- 中文详细：`docs/Chinese.md`
- 英文说明：`docs/English.md`
- 协议专题：`docs/Siemens.md`、`docs/Melsec.md`、`docs/ModbusTcp.md`、`docs/ModbusServer.md`、`docs/Omron.md`

---

如果需要，我可以在下一步继续补一份《二次开发规范（分支策略 + 兼容策略 + 回归模板）》放到 `docs/`。
