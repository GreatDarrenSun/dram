# MC小组能力建设路标
## ——传统研发版

## 一、能力建设总体目标

围绕MC研发及FPGA平台实现需求，建立：

**FPGA专业能力 + MC业务技术能力 + 组织资产**

三位一体的能力建设体系。

能力演进路径：

**基础能力  
→ 模块开发能力  
→ 子系统能力  
→ 系统架构能力  
→ 平台化能力**

最终目标：

> 建立具备MC架构设计、RTL实现、FPGA适配、功能验证、性能分析及问题定位能力的研发团队，并将项目过程中形成的技术成果、知识、方法和人才能力持续沉淀为组织资产。

---

# 二、FPGA专业能力建设

## L1：FPGA基础开发能力

重点掌握：

- SystemVerilog / Verilog
- FSM
- FIFO
- Pipeline
- RAM
- Counter
- Arbitration
- Clock / Reset
- 基础仿真
- 波形分析
- FPGA资源基础

目标：

> 能够独立完成模块级RTL设计、仿真和基本问题定位。

---

## L2：FPGA工程实现能力

### 1. Timing能力

掌握：

- Setup / Hold
- Clock Constraint
- IO Constraint
- Multicycle Path
- False Path
- Clock Group
- Timing Exception
- Critical Path分析
- Pipeline优化
- High Fanout优化

目标：

> 从“功能正确”提升到“功能正确 + 时序正确”。

### 2. CDC / RDC能力

掌握：

- Single Bit Synchronizer
- Pulse Synchronizer
- Handshake
- Async FIFO
- Reset Domain Crossing

建立：

- Clock Domain Map
- CDC Checklist
- RDC Checklist

### 3. FPGA资源与性能优化

掌握：

- LUT / FF
- BRAM / URAM
- DSP
- Resource Sharing
- Logic Duplication
- Register Retiming
- RAM推断
- Pipeline拆分

形成：

> Performance / Area / Timing综合权衡能力。

---

# 三、FPGA系统级能力

## L3：FPGA系统架构能力

重点建设：

### Clock Architecture

明确：

- Clock Source
- Clock Domain
- Clock Ratio
- Clock Crossing

### Reset Architecture

明确：

- Reset Source
- Reset Domain
- Reset Sequence
- Reset Release

### Data Path

掌握：

- Throughput
- Latency
- Pipeline
- Buffer
- Backpressure

### Control Path

掌握：

- Arbitration
- Dependency
- FSM
- Flow Control
- Deadlock Avoidance

### Debug Architecture

设计阶段预留：

- Counter
- Trace
- Trigger
- Timeout
- Error Monitor
- CSR
- ILA接口

目标：

> 从“出现问题以后再增加调试逻辑”，升级为“设计阶段即考虑可调试性”。

---

## L4：FPGA平台化能力

逐步形成：

- Clock / Reset Framework
- CSR Framework
- Debug Framework
- Trace Framework
- Traffic Generator
- CPGC
- Error Injection
- Performance Monitor

同时建设自动化：

- Build
- Simulation
- Regression
- Synthesis
- QoR统计
- 报告生成

最终形成：

> FPGA MC Development Platform。

---

# 四、MC业务技术能力建设

MC能力按照以下路径逐步构建：

**DRAM原理  
→ DDR协议  
→ Timing  
→ Bank Management  
→ Scheduler  
→ Data Path  
→ DFI  
→ System / Performance**

---

# 五、MC基础能力

## L1：DRAM原理与DDR协议

掌握：

- Rank
- Device
- Bank Group
- Bank
- Row
- Column
- Row Buffer
- Sense Amplifier
- Word Line
- Bit Line

深入理解：

- ACT
- RD
- WR
- PRE
- REF
- MRW / MRR

要求：

> 不仅知道命令怎么用，还能够解释命令及Timing背后的物理原因。

例如：

ACT  
→ Row Decode  
→ Wordline激活  
→ 电荷共享  
→ Sense Amplifier放大  
→ Row Buffer稳定

从而理解：

> 为什么ACT之后不能立即RD。

---

# 六、DDR Timing能力

## L2：Timing体系

建立：

### Bank Local Timing

例如：

- tRCD
- tRAS
- tRP
- tRTP
- tWR

### Bank Group / Rank / Global Timing

例如：

- tRRD
- tFAW
- tCCD
- tWTR

能力目标：

> 从Bank Local思维升级为Controller Global Timing思维。

形成：

### Command Dependency Matrix

明确：

- ACT → RD
- ACT → PRE
- PRE → ACT
- ACT → ACT
- RD → RD
- WR → RD
- RD → WR

对应的限制关系。

最终沉淀：

> DDR Timing Rule Database。

---

# 七、MC核心模块能力

## L3：MC模块开发能力

重点掌握以下模块。

### Request Frontend

处理：

- Read
- Write
- Address
- Priority
- Attribute

### Address Mapping

完成：

System Address

到：

Rank / BG / Bank / Row / Column

映射。

理解不同Mapping对：

- Row Hit Rate
- Bank Parallelism
- Performance

的影响。

### Bank Machine

维护：

- Bank State
- Open Row
- Pending Request
- Timing State

### Timing Manager

负责：

- Bank Timing
- BG Timing
- Rank Timing
- Global Timing

判断：

> 当前周期哪些命令允许发送。

### Scheduler

重点掌握：

- FCFS
- FR-FCFS
- Row Hit Priority
- Priority
- Aging
- Fairness
- QoS

能力演进：

**Correctness Scheduler**

↓

**Performance Scheduler**

### Refresh Manager

掌握：

- Refresh Request
- Refresh Deadline
- Refresh Arbitration

### Read / Write Data Path

掌握：

- Write Buffer
- Read Buffer
- Burst
- Alignment
- Transaction Tracking
- Return Path

### DFI

明确：

Host  
↓  
MC  
↓  
DFI  
↓  
PHY  
↓  
DRAM

各层职责边界。

---

# 八、MC系统与架构能力

## L4：系统级能力

重点建设：

- Initialization
- Training
- Power Management
- Self Refresh
- Frequency Change
- ECC
- CRC
- Error Handling
- RAS

进一步掌握完整的：

> Command Path + Data Path + Control Path + Timing Path。

---

# 九、MC性能能力

建立三类能力。

## Bandwidth

分析：

理论带宽

与

有效带宽

之间的差异。

重点分析：

- ACT / PRE
- Refresh
- Timing Bubble
- Bus Turnaround
- Scheduler效率

## Latency

形成：

Host Queue  
+ Scheduler  
+ DRAM Access  
+ Data Return

Latency Breakdown。

## Efficiency

关注：

- Row Hit Rate
- Bank Parallelism
- Bus Utilization
- Read / Write Turnaround
- Scheduler Efficiency

最终具备：

> 定位MC性能瓶颈并提出优化方案的能力。

---

# 十、组织资产建设

组织资产定义为：

> 团队在项目实践过程中沉淀形成、可持续复用和传承的技术成果、知识体系、研发方法及人才能力。

主要包括六类。

## 1. 设计资产

沉淀：

- MC总体架构
- Command Path
- Data Path
- Timing Path
- Interface Spec
- Design Spec
- RTL
- FPGA公共模块
- Clock / Reset框架
- Debug框架

---

## 2. 验证资产

沉淀：

- Testbench
- Test Case
- Assertion
- Coverage
- Regression
- Golden Case
- Error Injection
- Performance Benchmark

---

## 3. 知识资产

沉淀：

- DDR知识库
- DFI知识库
- Timing Rule Database
- Command关系图
- MC架构知识
- Issue / RCA库
- Debug经验
- 性能分析案例

---

## 4. 研发方法资产

形成标准：

- Architecture Review
- Design Review
- RTL Review
- Timing Review
- CDC / RDC Review
- Verification Review
- RCA机制
- 技术决策记录
- 项目复盘
- Coding规范
- Verification规范

---

## 5. 人才能力资产

建立：

- Skill Matrix
- 模块Owner
- Backup
- 专项专家
- Mentor
- 新人培养路径

人才梯队：

**模块开发者  
→ 模块Owner  
→ Subsystem Owner  
→ 专项专家  
→ MC Architect**

---

## 6. 项目经验资产

项目结束后形成：

- Top问题
- Top风险
- Top设计经验
- Top验证漏洞
- Top性能问题

形成闭环：

**Project  
→ Experience  
→ Standard  
→ Next Project**

实现：

> 项目做完以后，不只是留下代码，还要留下下一次可以直接使用的组织能力。

---

# 十一、能力建设阶段路标

## 0～3个月：基础打通

FPGA：

- Timing
- CDC / RDC
- Clock / Reset
- Debug基础

MC：

- DRAM原理
- DDR Command
- DDR Timing
- Bank State
- DFI基础

组织资产：

- MC架构图
- Timing Matrix
- Skill Matrix
- Owner初步划分
- Coding / Review规范

---

## 3～6个月：模块独立开发

重点模块：

- Address Mapping
- Bank Machine
- Timing Manager
- Refresh
- DFI Adapter

要求核心模块具备：

**Design + RTL + Test + Review**

组织资产同步形成：

- 模块Owner
- Backup
- Design Spec
- Test Case
- Issue / RCA

---

## 6～12个月：系统级能力

重点突破：

- Scheduler
- Data Path
- Init / Training
- Performance
- Regression体系

逐步形成：

- 子系统Owner
- Performance Benchmark
- Verification Library
- Debug方法库

---

## 12个月以后：架构与平台能力

建设：

- MC Architecture
- Scheduler Optimization
- QoS
- RAS
- Performance Architecture
- Debug Infrastructure

最终形成：

**MC RTL Platform  
+ Verification Platform  
+ Debug Platform  
+ Knowledge Platform**

团队从：

> 项目交付型团队

升级为：

> MC技术平台型团队。