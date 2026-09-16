# DDR6 FPGA-Based SLT
# 跨部门 MC / PHY 资料需求提炼提示词

## 一、任务背景

我们正在建设 **DDR6 FPGA-Based SLT 平台**。

当前需要从本部门已有资料中，系统提取与 DDR6 Memory Controller（MC）、PHY、DFI、Training 以及相关 SLT 测试能力有关的需求，并合入统一的 DDR6 SLT 需求池。

目前不预设本部门资料形式。

资料可能包括：

- Word
- PPT
- Excel
- Markdown
- PDF
- 设计文档
- 架构文档
- 接口协议
- 寄存器说明
- 测试方案
- Test Case
- 测试记录
- Bug / Issue
- 会议纪要
- 邮件导出
- 代码
- Header
- 配置文件
- 脚本
- Log
- README
- 历史项目资料

因此本轮首先需要做资料摸底，再提炼需求。

---

# 二、核心任务

最终目标不是总结文档内容，而是回答：

> 本部门过去或当前对 DDR6 MC、PHY 以及 SLT 平台到底提出过哪些实际需求？

需要完成：

```text
资料扫描
    ↓
识别与DDR6 SLT有关的信息
    ↓
区分“需求 / 设计 / 测试 / 问题 / 背景”
    ↓
提取真正的需求
    ↓
标准化需求表达
    ↓
按照统一需求分类归档
    ↓
去重
    ↓
发现冲突
    ↓
发现需求缺口
    ↓
形成统一需求表
```

---

# 三、范围约束

本轮正式需求范围：

**仅 DDR6。**

如果资料中出现：

- DDR5
- LPDDR5
- LPDDR6
- GDDR
- HBM
- 其他历史 Memory 项目

不要直接合入 DDR6 需求。

可以把它们作为：

`REFERENCE_ONLY`

只有资料明确说明该能力也适用于 DDR6，或者能够证明这是 DDR6 当前项目正在沿用的需求时，才可以进入 DDR6 需求池。

必须标明来源和适用范围。

---

# 四、先做资料清点

先递归扫描给定资料目录。

生成：

`00_SOURCE_INVENTORY.md`

格式：

| SOURCE_ID | 文件 | 类型 | 版本/日期 | 主要内容 | 是否涉及DDR6 | 是否涉及MC | 是否涉及PHY | 是否涉及SLT | 需求价值 | 备注 |
|---|---|---|---|---|---|---|---|---|---|---|

需求价值分为：

- HIGH：存在明确需求、接口、参数、测试条件或验收要求
- MEDIUM：存在设计约束或测试行为，可以反推需求
- LOW：主要为背景资料
- NONE：与本任务无关

不要因为文件名看起来无关就直接跳过。

应先检查内容。

---

# 五、必须区分五种信息

资料中的内容必须先分类为：

### 1. REQUIREMENT

真正要求系统必须具备的能力。

例如：

> MC需要支持DDR6某种Refresh模式。

---

### 2. DESIGN

现有或历史实现方式。

例如：

> 当前设计采用4级FIFO。

这不一定是需求。

不能直接写成：

> 系统必须采用4级FIFO。

---

### 3. TEST

测试方法、Test Case或验证手段。

例如：

> 使用某Pattern测试DQ稳定性。

需要进一步判断它背后对应什么系统能力需求。

---

### 4. ISSUE

历史Bug、问题、限制或异常。

例如：

> 某Training场景失败。

不能直接当成需求。

但需要检查它是否暴露了：

- 缺失能力
- 边界条件
- Debug需求
- 状态可观测性需求

---

### 5. BACKGROUND

背景知识、协议介绍、行业资料等。

不能直接进入需求池。

---

# 六、统一一级需求分类

所有正式需求统一映射到以下六个一级分类。

禁止因为原文使用其他叫法就重新建立另一套一级分类。

---

## 01 测试控制与平台支撑

包括但不限于：

- 测试启动/停止
- 配置下发
- 状态查询
- 软件控制
- Host接口
- FPGA控制
- 自动化执行
- 日志
- 数据回读
- Trigger
- 多通道测试控制
- 测试流程管理

---

## 02 DDR6控制器与协议

这是 MC 需求的主要归属。

重点检查：

### 初始化与配置

- Reset
- Initialization
- MR
- FSP
- Mode配置
- Feature Enable/Disable

### DDR6协议能力

- ACT
- PRE
- RD
- WR
- REF
- MRW/MRR
- ZQ
- Power Down
- Self Refresh
- Direct Command

### 地址与组织

- Channel
- Sub-channel
- Rank
- Bank
- Bank Group
- Row
- Column
- PSD
- BL
- Address Mapping

### Timing

检查所有：

- ACT相关Timing
- RD/WR相关Timing
- PRE相关Timing
- Refresh相关Timing
- Rank切换Timing
- Bank相关Timing
- Bus Turnaround
- Write/Read Latency
- 其他DDR6 Timing约束

### Scheduler / Arbitration

- Command调度
- Bank调度
- Priority
- Reorder
- No-Reorder
- Dependency
- Outstanding
- Row-hit
- Fairness

### Refresh

- Refresh类型
- Refresh控制
- Refresh调度
- Refresh暂停/插入
- 与测试流量关系

### 其他

- ODT
- Latency
- CRC
- Metadata
- Error/Retry
- Feature开关
- 协议状态
- 异常恢复

---

## 03 PHY / DFI 与训练

这是 PHY 相关需求的主要归属。

重点检查：

### MC ↔ PHY接口

- DFI或DFI-like接口
- Command
- Address
- Write Data
- Read Data
- Data Mask
- Status
- Training Control
- Training Result
- Handshake
- Backpressure

### Clock / Reset

- MC Clock
- PHY Clock
- DFI Clock
- Clock Ratio
- Reset
- Reset Sequence
- CDC

### CA / CK / CS

- CK
- CS
- CA
- Command Timing
- Delay
- Phase

### TX数据路径

- DQ
- DQS
- Data Serialization
- TX Delay
- Phase
- Alignment

### RX数据路径

- DQ
- DQS
- Sampling
- RX Delay
- Capture Window
- Alignment

### IO配置

- Ron
- ODT
- Drive Strength
- Slew
- IO Delay
- Voltage相关控制

### Training

检查所有训练：

- 初始化训练
- Read Training
- Write Training
- DQS相关训练
- CA相关训练
- Vref相关训练
- Leveling
- Calibration
- Re-training
- Training Trigger
- Training状态
- Training失败原因
- Training Result回读

### PHY可观测性

- Delay值
- Tap值
- Window
- Margin
- Pass/Fail
- Training阶段
- Error Reason

---

## 04 CPGC / 测试算法

只保留与 MC / PHY 测试直接相关的内容。

包括：

- Address Pattern
- Data Pattern
- Read/Write Sequence
- Traffic Pattern
- Loop
- PRBS
- Checkerboard
- Walking Pattern
- Stress Pattern
- Compare
- Expected Data
- Error Injection
- Test Sequence

如果只是 CPGC 自身内部实现，而与本部门 MC/PHY需求没有关系，可以不展开。

---

## 05 系统、裕量与兼容性测试

包括：

### 系统功能测试

- 基础读写
- 长时间运行
- 满带宽
- 多Bank
- 多Rank
- 多Channel
- 压力测试
- Corner测试

### 裕量测试

- Timing Margin
- Voltage Margin
- Delay Sweep
- Vref Sweep
- Frequency Sweep
- Shmoo
- Window测试

### 兼容性

- 不同Die
- 不同DIMM/Device
- 不同速率
- 不同配置
- 不同板卡
- 不同PHY参数
- 不同MC配置

### 板级相关

- SI相关测试要求
- Board Variation
- Channel Variation
- IO Margin

---

## 06 故障诊断与可靠性

包括：

### 故障定位

- Fail Address
- Fail Data
- Expected Data
- Actual Data
- DQ Bitmap
- Channel
- Rank
- Bank
- Row
- Column
- Beat
- Burst

### Debug

- MC状态
- PHY状态
- Training状态
- Command Trace
- Data Trace
- Counter
- Snapshot
- Event Record

### RAS / Reliability

- Error Counter
- CRC Error
- Retry
- Recovery
- Timeout
- Error Threshold
- Error Injection
- Long Run
- Reliability
- 可恢复/不可恢复错误

---

# 七、MC与PHY需求必须继续细分二级分类

不要只写：

> DDR6控制器与协议

或者：

> PHY/DFI与训练

必须给出二级分类。

例如：

```text
DDR6控制器与协议
 ├─ 初始化与配置
 ├─ 地址与组织
 ├─ 命令与协议
 ├─ Timing
 ├─ Scheduler与仲裁
 ├─ Refresh
 ├─ MR/FSP
 ├─ ODT/ZQ
 ├─ 低功耗
 ├─ Latency
 └─ Error/Recovery
```

PHY：

```text
PHY/DFI与训练
 ├─ MC-PHY接口
 ├─ Clock/Reset
 ├─ CA/CK/CS
 ├─ Write Path
 ├─ Read Path
 ├─ IO配置
 ├─ Delay/Phase
 ├─ Training
 ├─ Re-training
 ├─ Calibration
 └─ Status/Debug
```

如果现有需求无法归入以上二级分类：

不要硬塞。

标记：

`SECONDARY_CATEGORY_TBD`

并说明为什么。

---

# 八、重点寻找 MC ↔ PHY 跨模块需求

这是本轮必须单独完成的一项。

很多需求不能简单归到 MC 或 PHY，因为真正关键的是双方接口合同。

重点寻找：

- MC负责什么
- PHY负责什么
- Training谁控制流程
- Training谁执行物理动作
- Command由谁生成
- Delay由谁配置
- Timing由谁保证
- Read Data什么时候有效
- Write Data什么时候发出
- Status什么时候返回
- Error怎么反馈
- Backpressure如何处理
- Clock Ratio
- Reset顺序
- Re-initialization
- Re-training
- Timeout
- Fail Recovery

输出：

`04_MC_PHY_INTERFACE_AND_OWNERSHIP.md`

格式：

| ITEM_ID | 功能 | MC职责 | PHY职责 | 接口信息 | 时序要求 | 状态/反馈 | 来源 | 未决问题 |
|---|---|---|---|---|---|---|---|---|

如果资料没有明确规定 Ownership：

写：

`UNKNOWN`

禁止自行决定。

---

# 九、需求标准化

所有真正的需求必须重新写成工程需求语言。

不要直接复制原文。

例如原文：

> 这个训练最好可以重新跑一下。

标准化成：

> PHY应支持在不重新进行完整系统上电初始化的情况下，由MC或Host触发指定Training流程重新执行。

如果“无需完整初始化”并没有代码或文档证据，则不能加入这一条件。

必须严格按照原始证据表达。

---

# 十、统一需求主表

最终生成：

`01_DDR6_SLT_REQUIREMENTS_MASTER.csv`

字段固定为：

```text
需求ID
一级分类
二级分类
需求名称
详细需求描述
关键配置/控制点
执行层级
责任模块
建议优先级
验收方法
验收输出/证据
依据来源
来源位置
证据等级
边界/备注
```

---

# 十一、字段解释

## 需求ID

统一格式，例如：

```text
MC-REQ-001
PHY-REQ-001
IF-REQ-001
SYS-REQ-001
DBG-REQ-001
```

---

## 执行层级

只能从以下范围选择：

```text
Host/Software
FPGA Test Engine
MC
MC-PHY Interface
PHY
Board/System
Cross-Layer
```

---

## 责任模块

写真正负责实现该能力的模块。

例如：

```text
MC
PHY
MC+PHY
Host
CPGC
Board
TBD
```

不要因为文档是谁写的就把谁当 Owner。

---

## 建议优先级

使用：

```text
P0
P1
P2
TBD
```

如果原始资料无法支持优先级判断，不要凭感觉决定，填：

`TBD`

---

## 证据等级

使用：

### SOURCE_CONFIRMED

原文明确提出需求。

### BEHAVIOR_CONFIRMED

原文没有写“需求”，但测试、接口或行为明确证明必须有该能力。

### INFERRED

可以合理推断，但需要负责人确认。

### UNKNOWN

当前资料不足。

---

# 十二、不要遗漏隐藏需求

除了显式写有“要求”“需要”“支持”的内容，还需要主动寻找隐藏需求。

例如：

### 从接口定义反推

如果接口中存在：

```text
training_start
training_done
training_fail
```

则说明可能存在：

- Training Trigger
- Training完成状态
- Training失败状态

但必须标记证据来源。

---

### 从Test Case反推

如果Test Case要求：

> 不同Vref循环Sweep并记录Pass Window

则可能对应：

- Vref可配置
- Vref动态更新
- 测试执行期间重复配置
- Pass Window结果获取

但需要区分：

`BEHAVIOR_CONFIRMED`

或：

`INFERRED`

---

### 从Bug反推

如果Issue中写：

> Retraining后MC状态未恢复。

可能说明：

- Re-training
- MC/PHY状态同步
- Training后恢复流程

存在需求。

但不能把具体Bug现象直接当需求。

---

# 十三、去重规则

不同文档可能表达同一个需求。

例如：

```text
支持Read Training
支持RX Training
支持读DQ采样窗口训练
```

不要直接生成三条需求。

需要判断：

- 是否同一能力；
- 是否上下级关系；
- 是否不同参数；
- 是否不同场景。

同一需求合并后保留所有来源。

---

# 十四、冲突识别

如果不同资料对同一需求给出不同结论：

例如：

```text
文档A：DFI Ratio = 1:4
文档B：DFI Ratio = 1:8
```

禁止自行选择一个。

标记：

`CONFLICT`

输出到：

`05_REQUIREMENT_CONFLICTS.md`

格式：

| CONFLICT_ID | 需求 | 来源A | 来源B | 冲突内容 | 对架构影响 | 需要谁确认 |
|---|---|---|---|---|---|---|

---

# 十五、Open Questions

所有以下问题统一进入：

`06_OPEN_QUESTIONS.md`

包括：

- 资料没有说明；
- 多文档冲突；
- Owner不清楚；
- 参数没有范围；
- Timing没有值；
- Feature是否必须支持不清楚；
- MC/PHY边界不清楚；
- Training流程不完整；
- 验收标准不明确。

格式：

| Q_ID | 问题 | 来源 | 影响需求 | 为什么必须确认 | 建议确认对象 |
|---|---|---|---|---|---|

---

# 十六、输出 MC 专项需求

生成：

`02_MC_REQUIREMENTS.md`

按以下结构整理：

```text
1. 初始化与配置
2. 地址与组织
3. 命令与协议
4. Timing
5. Scheduler / Arbitration
6. Refresh
7. MR / FSP
8. ODT / ZQ
9. Latency
10. Power Management
11. Error / Recovery
12. Debug / Observability
13. 与CPGC关系
14. 与PHY关系
15. Open Questions
```

每项引用统一需求ID。

---

# 十七、输出 PHY 专项需求

生成：

`03_PHY_REQUIREMENTS.md`

按以下结构整理：

```text
1. MC-PHY / DFI接口
2. Clock / Reset
3. CK / CS / CA
4. Write Data Path
5. Read Data Path
6. Delay / Phase
7. IO配置
8. Training
9. Calibration
10. Re-training
11. Status / Error
12. Debug / Observability
13. Margin支持
14. 与MC关系
15. Open Questions
```

每项引用统一需求ID。

---

# 十八、寻找我们当前需求池中可能缺失的内容

不能只把资料硬塞进已有需求。

完成抽取后，再站在 MC / PHY 工程角度检查：

> 本部门资料里是否存在我们当前统一需求分类已经能够容纳，但以前需求池中没有覆盖的具体能力？

输出：

`07_REQUIREMENT_GAPS.md`

格式：

| GAP_ID | 发现的新需求点 | 一级分类 | 二级分类 | 来源 | 为什么以前可能遗漏 | 是否建议纳入 |
|---|---|---|---|---|---|---|

注意：

这里的“新”仅表示：

> 相对于当前需求池可能缺失。

不要在最终需求表中标注“新增/增强/沿用”。

---

# 十九、最终汇总

生成：

`08_REQUIREMENT_SUMMARY.md`

只回答：

### 1. 共扫描多少资料？

### 2. 识别多少条有效DDR6需求？

### 3. MC需求多少条？

### 4. PHY需求多少条？

### 5. MC-PHY跨模块需求多少条？

### 6. 六个一级分类分别多少条？

### 7. 有多少：
- SOURCE_CONFIRMED
- BEHAVIOR_CONFIRMED
- INFERRED
- UNKNOWN

### 8. 有多少重复需求被合并？

### 9. 有多少冲突？

### 10. 有多少Open Questions？

### 11. 当前影响DDR6 SLT总体方案最大的Top问题是什么？

Top问题只能按：

> 对架构影响范围

整理。

不要自行修改需求优先级。

---

# 二十、最终交付文件

必须输出：

```text
00_SOURCE_INVENTORY.md

01_DDR6_SLT_REQUIREMENTS_MASTER.csv

02_MC_REQUIREMENTS.md

03_PHY_REQUIREMENTS.md

04_MC_PHY_INTERFACE_AND_OWNERSHIP.md

05_REQUIREMENT_CONFLICTS.md

06_OPEN_QUESTIONS.md

07_REQUIREMENT_GAPS.md

08_REQUIREMENT_SUMMARY.md
```

---

# 二十一、最重要的约束

本轮禁止：

1. 因为DDR6规范里有某功能，就默认项目需要支持。
2. 因为Intel/AMD/JEDEC/其他产品有某能力，就自行加入需求。
3. 把现有设计实现直接当成需求。
4. 把Bug描述直接当成需求。
5. 把Test Case直接复制成需求。
6. 根据个人经验自行确定MC/PHY Ownership。
7. 自行决定接口位宽、FIFO深度、Buffer深度。
8. 自行决定Training实现方式。
9. 自行决定Timing值。
10. 自行解决不同资料之间的冲突。
11. 把DDR5/LPDDR6需求直接混入DDR6需求。
12. 为了让分类完整而编造需求。

最终所有正式需求必须做到：

> 有来源、有分类、有边界、有Owner状态、有证据等级、能够被后续 FPGA/MC/PHY 方案继续使用。