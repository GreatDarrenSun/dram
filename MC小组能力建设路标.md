# MC小组能力建设路标

## 一、能力建设总体目标

围绕 DDR6 FPGA Based SLT / MC 开发需求，建立“**FPGA专业能力 + MC业务技术能力**”双能力体系。

能力建设不以单纯掌握知识点为目标，而是逐步形成：

**阶段1：掌握基础，能够看懂和定位问题**  
↓  
**阶段2：独立承担模块设计、开发与验证**  
↓  
**阶段3：具备MC子系统架构设计和端到端问题闭环能力**  
↓  
**阶段4：形成团队方法论、设计资产和技术平台，实现能力复制**

最终目标：

> 建立一支能够独立完成 DDR MC 架构设计、RTL实现、FPGA适配、功能验证、性能分析及问题定位的研发团队，并形成可复用的 MC 设计与验证平台。

---

# 二、能力体系

整体能力划分为两条主线：

**专业技能：FPGA工程能力**

重点解决：

> “如何把MC高质量、高性能、稳定地实现在FPGA上。”

**业务技术：Memory Controller能力**

重点解决：

> “MC为什么这样设计，以及如何正确、高效地控制DDR。”

两条能力最终在MC工程实践中汇合。

---

# 三、专业技能路线——FPGA

## L1：FPGA基础工程能力

目标：

能够独立完成模块级RTL设计、仿真和基本调试。

重点能力：

- SystemVerilog / Verilog RTL设计
- FSM、Pipeline、FIFO、RAM等基础结构
- 同步设计原则
- Reset设计
- Clock Domain Crossing
- 基础仿真与波形分析
- FPGA资源基本认识
  - LUT
  - FF
  - BRAM
  - URAM
  - DSP
- 基本综合、实现流程

阶段输出：

- FPGA编码规范
- RTL Review Checklist
- CDC Checklist
- 基础模块库

---

## L2：复杂FPGA设计能力

目标：

能够承担MC核心模块FPGA实现。

重点能力：

### 1. 时序设计

掌握：

- Setup / Hold
- Clock uncertainty
- Clock skew
- Multicycle Path
- False Path
- Clock Groups
- Input / Output Delay
- Timing Exception

能够完成：

- Timing Constraint
- Timing Report分析
- Critical Path定位
- Pipeline优化
- 高Fanout优化

核心目标：

> 从“功能正确”提升到“功能 + 时序正确”。

---

### 2. 多时钟与跨时钟设计

重点掌握：

- CDC
- Async FIFO
- Pulse Sync
- Reset Domain Crossing
- Clock Ratio变化
- Gearbox / Ratio转换

结合MC重点关注：

- Controller Clock
- DFI Clock
- PHY Clock
- Host Clock

之间的数据和命令传递。

---

### 3. FPGA性能与资源优化

掌握：

- Pipeline拆分
- Register Retiming
- RAM推断
- Logic Duplication
- Resource Sharing
- Critical Path优化

建立：

**Performance / Area / Timing Trade-off能力**

即：

> 不仅知道RTL怎么写，还知道怎样写更适合FPGA。

---

## L3：FPGA系统架构能力

目标：

能够从系统角度设计大型MC FPGA架构。

重点能力：

- 多模块时钟规划
- Reset架构
- 数据流规划
- 控制流规划
- FPGA资源预算
- 带宽预算
- Latency Budget
- Debug架构设计

尤其需要建立：

### Design for Debug

在设计阶段预埋：

- Performance Counter
- Error Counter
- Command Trace
- State Trace
- Trigger
- Timeout Monitor
- ILA Probe
- Debug Register

目标：

> 从“出现问题再加ILA”转变为“设计时就考虑如何定位问题”。

---

## L4：FPGA平台化能力

目标：

MC不再是一次性项目，而形成可持续演进的平台。

形成：

- 通用Clock / Reset框架
- 通用CSR框架
- 通用Debug框架
- 通用DFI接口层
- 通用Memory Traffic Generator
- 通用CPGC
- 通用Trace
- 通用Error Injection
- 通用Performance Monitor

同时建设自动化：

- Python
- Tcl
- Regression
- CI
- 自动Build
- 自动仿真
- 自动报告
- 自动QoR统计

最终形成：

> FPGA MC Development Platform

---

# 四、业务技术路线——Memory Controller

MC能力建设建议按照：

**DRAM原理 → 协议 → Timing → Command → Scheduler → Data Path → 系统性能**

逐层深入。

---

# L1：DRAM基本原理

目标：

真正理解DDR命令背后的物理原因，而不是单纯背JEDEC参数。

重点掌握：

### DRAM组织结构

理解：

DIMM / Rank  
↓  
Device  
↓  
Bank Group / Bank  
↓  
Row  
↓  
Column

理解：

- Row Buffer
- Sense Amplifier
- Word Line
- Bit Line

---

### 基础命令

深入理解：

- ACT
- RD
- WR
- PRE
- REF
- MRW / MRR

不仅知道命令定义，还要理解：

例如：

ACT为什么需要tRCD？

因为背后存在：

Row Decode  
→ Wordline激活  
→ Cell电荷共享  
→ Sense Amplifier放大  
→ Row Buffer稳定

目标：

> 每一个关键Timing都能够解释其物理或协议来源。

---

# L2：DDR Timing体系

这是MC最核心的能力之一。

建议建立完整Timing知识图谱。

## Bank Local Timing

例如：

- tRCD
- tRAS
- tRP
- tRTP
- tWR

理解：

> 同一个Bank内部命令之间为什么存在限制。

---

## Rank / Bank Group Timing

例如：

- tRRD
- tFAW
- tCCD
- tWTR

理解：

> 为什么Bank1即使是Closed，也不代表一定可以立即ACT。

从：

**Bank Local思维**

升级到：

**Controller Global Timing思维。**

---

## Read / Write方向切换

深入理解：

- RD → WR
- WR → RD

为什么会有限制。

建立：

**Command Dependency Matrix**

例如：

| 前命令 | 后命令 | Timing约束 |
|---|---|---|
| ACT | RD | tRCD |
| ACT | PRE | tRAS |
| PRE | ACT | tRP |
| ACT | ACT | tRRD / tFAW |
| RD | RD | tCCD |
| WR | RD | tWTR |
| RD | WR | Bus Turnaround |

最终形成：

> MC Timing Rule Database

作为Scheduler设计的基础。

---

# L3：MC核心架构

开始进入真正Controller设计。

重点学习和掌握以下模块。

## 1. Request Frontend

处理：

Host Request

包括：

- Read
- Write
- Address
- Length
- Priority
- Attribute

---

## 2. Address Mapping

完成：

System Address

到：

- Rank
- Bank Group
- Bank
- Row
- Column

的映射。

需要理解：

不同Mapping策略对：

- Row Hit Rate
- Bank Parallelism
- Performance

的影响。

---

## 3. Bank Machine

每个Bank维护：

- Open / Closed状态
- Open Row
- Pending Request
- Timing State

负责：

ACT / PRE / RD / WR

等基本决策。

---

## 4. Timing Manager

集中维护DDR Timing状态。

例如：

- last_ACT
- last_RD
- last_WR
- tFAW window
- Rank timing
- Bank Group timing

判断：

> 当前周期哪些Command合法。

这是MC核心基础模块之一。

---

## 5. Command Scheduler

这是MC能力建设的重点。

Scheduler需要解决：

多个合法Command同时存在时：

> 到底选择哪个Command发送？

需要理解：

- FCFS
- FR-FCFS
- Row Hit优先
- Read / Write优先
- Aging
- Priority
- Fairness
- QoS

逐步建立：

**Correctness → Performance**

两层Scheduler思维。

---

## 6. Refresh Manager

掌握：

- Refresh Request
- Refresh Deadline
- Refresh Arbitration
- Refresh与Normal Traffic冲突

同时理解：

Refresh为什么会影响：

- Latency
- Bandwidth
- QoS

---

## 7. Read / Write Data Path

掌握：

Command Path

和

Data Path

之间的对应关系。

理解：

- Write Data Buffer
- Read Data Buffer
- Data Alignment
- Burst管理
- Transaction ID
- Return Path

解决：

> Command什么时候发送，Data什么时候到达。

---

## 8. DFI / PHY接口

建立清晰边界：

Host  
↓  
MC  
↓  
DFI  
↓  
PHY  
↓  
DRAM

重点理解：

- Command
- Address
- Write Data
- Read Data
- Training
- Init
- Frequency Ratio

明确：

**MC负责什么、PHY负责什么。**

---

# L4：MC系统能力

这一阶段目标：

> 不再只看单模块，而是能够分析整个MC行为。

重点包括：

## Initialization

完整掌握：

Power Up  
→ Reset  
→ Mode Register配置  
→ Training  
→ Normal Operation

---

## Training

理解：

MC和PHY在Training中的职责边界。

例如：

- Training Sequence
- Pattern
- MR配置
- Training Result
- Training State

---

## Power Management

掌握：

- Power Down
- Self Refresh
- Clock管理
- Frequency Change

---

## Reliability / RAS

逐步建设：

- ECC
- CRC
- Retry
- Error Detection
- Error Injection
- Error Reporting

---

# 五、MC高级能力——性能与架构

当功能正确后，需要进一步建设：

> MC性能分析能力。

掌握三个核心指标：

### Bandwidth

理论带宽

vs

有效带宽。

分析损失来源：

- ACT / PRE
- Refresh
- Bus Turnaround
- Timing Bubble
- Scheduler效率

---

### Latency

拆分：

Host Queue Latency  
+  
Scheduler Latency  
+  
DRAM Access Latency  
+  
Data Return Latency

形成：

**Latency Breakdown能力。**

---

### Efficiency

例如：

Bus Utilization

Row Hit Rate

Bank Parallelism

Read / Write Turnaround

最终能够回答：

> 为什么理论100%的带宽，实际只有70%？

而不是只看到结果。

---

# 六、能力建设时间路标

建议按照四个阶段推进。

## 第一阶段：0～3个月

主题：

**基础打通**

FPGA重点：

- CDC / Reset
- Timing Constraint
- FPGA Timing分析
- Debug方法
- MC FPGA工程结构

MC重点：

- DRAM原理
- DDR Command
- DDR Timing
- Bank State
- DFI基础

完成：

- MC整体架构图
- DDR Command知识图
- DDR Timing关系图
- MC Timing Matrix
- MC模块职责地图

目标：

> 团队成员能够看懂MC，并能够进行基本问题定位。

---

# 第二阶段：3～6个月

主题：

**模块独立开发**

重点模块：

- Address Mapping
- Bank Machine
- Timing Manager
- Refresh Manager
- DFI Adapter

FPGA同时强化：

- Pipeline
- Timing Closure
- CDC
- Resource Optimization

完成：

每个核心模块至少形成：

**设计文档 + RTL + Testbench + Review Checklist**

目标：

> 团队成员能够独立承担MC模块开发。

---

# 第三阶段：6～12个月

主题：

**MC系统设计能力**

重点突破：

- Scheduler
- Read / Write Data Path
- Refresh Arbitration
- Init / Training
- Performance Counter

建立：

- MC Regression
- MC Assertion
- Coverage
- Traffic Generator
- Performance Benchmark

目标：

> 团队具备端到端MC开发和问题闭环能力。

---

# 第四阶段：12个月以后

主题：

**架构与平台能力**

重点建设：

- MC Performance Architecture
- Scheduler优化
- QoS
- 多Rank / 多Channel
- RAS
- Debug Infrastructure
- MC通用架构

沉淀：

MC RTL Platform  
+  
MC Verification Platform  
+  
MC Debug Platform  
+  
MC Knowledge Base

目标：

> 从“项目开发团队”升级为“MC技术平台团队”。

---

# 七、团队梯队建设

作为MC负责人，建议建立三级人员梯队。

## Level A：模块开发者

要求：

能够独立承担一个MC模块。

例如：

- Bank Machine
- Refresh
- Address Mapping
- DFI

---

## Level B：子系统Owner

要求：

能够负责一条完整功能链路。

例如：

Host Request  
→ Scheduler  
→ Command  
→ DFI

能够完成：

设计  
+  
验证  
+  
Debug  
+  
问题闭环。

---

## Level C：MC Architect

要求：

能够进行：

- MC Architecture
- Timing Architecture
- Scheduler Architecture
- Performance Architecture
- DFI / PHY Interface Architecture

并能够进行跨模块问题分析。

团队目标：

> 核心模块至少做到“一主一备”，避免单点能力。

---

# 八、团队资产建设

能力建设不能只存在于个人脑子里。

建议长期维护六类资产。

### 1. MC Architecture Library

包括：

- MC总体架构图
- Command Path
- Data Path
- Timing Path
- DFI Interface

### 2. DDR Timing Database

形成DDR Timing规则库。

### 3. MC Design Spec

核心模块均有标准设计文档。

### 4. MC Verification Library

包括：

- Test Case
- Assertion
- Coverage
- Regression

### 5. MC Issue / RCA Library

每一个复杂问题记录：

现象  
→ 定位过程  
→ Root Cause  
→ Fix  
→ Prevention

逐步形成：

**MC故障知识库。**

### 6. MC Review Checklist

分别建立：

- Architecture Review
- RTL Review
- Timing Review
- CDC Review
- Verification Review
- Performance Review

---

# 九、能力建设评价指标

避免仅用“培训次数”衡量能力建设。

建议采用工程成果评价。

## FPGA能力指标

关注：

- Timing Closure
- CDC问题数量
- RTL缺陷率
- FPGA资源利用率
- Critical Path数量
- Debug效率

---

## MC能力指标

关注：

- Timing Rule覆盖率
- Protocol Assertion覆盖率
- MC模块独立开发能力
- Regression通过率
- Corner Case覆盖率
- Root Cause定位能力
- Performance达成率

---

## 团队能力指标

关注：

- 核心模块Owner覆盖率
- 核心模块Backup覆盖率
- 设计文档覆盖率
- Review覆盖率
- 自动化Regression覆盖率
- 技术资产复用率

---

# 十、最终能力建设目标

MC小组能力建设最终形成三层能力：

**第一层：工程实现能力**

FPGA RTL / Timing / CDC / Debug / Verification

↓

**第二层：MC业务能力**

DDR Protocol / Timing / Scheduler / Data Path / DFI

↓

**第三层：系统架构能力**

Performance / Reliability / Architecture / Platform

最终实现：

> 从“会做FPGA的MC团队”，逐步建设成为“理解DRAM本质、具备MC架构能力，并能够在FPGA平台上高质量实现和验证MC的专业团队”。