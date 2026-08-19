# Unknown List

## Priority: HIGH (Blocking further analysis)

| ID | Question | Current Evidence | Missing Evidence | Next Action |
|----|----------|------------------|------------------|-------------|
| U-001 | Which scheduler path is active? ts/gs/bsm vs. PAS (pascc/pasci/pasds) | Both exist in RTL; `dwc_ddrctl_ddrc_cpe` instantiates `ts`; `dwc_ddrctl_pas_cpe` also instantiated | `GEN_DDRC_CPE_EN` value; generate block conditions | Read cc_constants for GEN_DDRC_CPE_EN; read CP instantiation generate |
| U-002 | DDR5 mode or DDR4 mode? | `ddrc_ddr4_mode` port selects; `MEMC_DDR4_EN=1`, `MEMC_DDR5_ONLY_EN=0` | Actual runtime value; simulation testbench config | Check simulation scripts; check register default |
| U-003 | How does XPI connect to CPF/CPE? | XPI in arb_top and separate module; large xpi.sv (6368 LOC) | HIF bus path from arb_top to ddrc; XPI internal hierarchy | Read xpi.sv to understand connection topology |
| U-004 | Is ECC enabled? | `MEMC_SECDED_ECC_WIDTH_BITS=8` defined; `MEMC_ECC_SUPPORT` unknown | `MEMC_ECC_SUPPORT` value in cc_constants remaining lines | Read cc_constants lines 15300-17450 |
| U-005 | Single or dual channel? | No dual-channel ports seen in top; `MEMC_WDATARAM1_EXISTS=0` | `UMCTL2_DUAL_CHANNEL` value | Read cc_constants for dual channel config |
| U-006 | Number of ranks? | Not yet found in cc_constants lines read | `MEMC_NUM_RANKS` value | Read cc_constants |

## Priority: MEDIUM (Can work around)

| ID | Question | Current Evidence | Missing Evidence | Next Action |
|----|----------|------------------|------------------|-------------|
| U-007 | Bank/BG/ROW/COL configuration | Not in read portions of cc_constants | `MEMC_BANK_BITS`, `MEMC_BG_BITS`, `MEMC_PAGE_BITS`, `MEMC_BLK_BITS` | Read cc_constants |
| U-008 | PAS subsystem exact purpose | Has cc/ci/ds/gs/lc/os/pi/du subdirs paralleling ts/gs/bsm | Whether it's DDR5-only or common; how muxed | Read pas_cpe.sv instantiation conditions |
| U-009 | dfi_rolling_order_rst purpose | Declared in DWC_ddrctl.sv:6089 | Where driven; what it controls | Trace signal driver |
| U-010 | Write data RAM address mapping | `MEMC_WDATARAM0_EXISTS=1`; wdataram_* ports at top level | How memc_wu interfaces with external RAM | Read memc_wu_wdata_if.sv |
| U-011 | Retry path: CRC vs Parity | retry_ctrl.sv exists; `MEMC_DDR5_OR_DDRCTL_RD_CRC_RETRY` in undef | Which retry mechanism is active | Read retry_ctrl.sv |
| U-012 | ODT control mechanism | gs_odt.sv exists | DDR5 ODT vs DDR4 ODT differences | Read gs_odt.sv |
| U-013 | ZQ calibration flow | gs_zq_calib.sv exists; perf_op_is_zqstart/zqlatch signals | DDR5 ZQ vs DDR4 ZQ differences | Read gs_zq_calib.sv |
| U-014 | MRW/MRR DDR5 encoding | mr.sv has `ifdef MEMC_DDR5` (line 635) | DDR5 mode register specific handling | Read mr.sv |
| U-015 | Bypass evaluation criteria | bypass.sv (195 LOC) | What transactions are eligible for bypass | Read bypass.sv |

## Priority: LOW (Nice to have)

| ID | Question | Current Evidence | Missing Evidence | Next Action |
|----|----------|------------------|------------------|-------------|
| U-016 | Performance counters | perf_* signals (40+) in top module | How performance counters are implemented | Read CPE performance hooks |
| U-017 | Debug signals | dbg_* ports at top level | Purpose of each debug signal | Read top module comments |
| U-018 | Write combine feature | perf_write_combine signal | How write combine works | Read memc_wu.sv for write combining |
| U-019 | QoS mechanism | xpi_qos.sv (122 LOC) | QoS priority scheme | Read xpi_qos.sv |
| U-020 | Dynamic scheduling | pasgs_dyn_sched.sv (138 LOC) | Dynamic scheduling algorithm | Read module |
| U-021 | Register map content | apb_coreif.sv (12,504 LOC) | Complete register map documentation | Read apb_defines.svh |
| U-022 | CHB config constants | chb_cc_constants.svh (NOT_READ) | Not applicable (CHB disabled) | Skip unless needed |
| U-023 | DFI package encoding | dfi_pkg.svh (NOT_READ) | DFI command encoding definitions | Read for command pipeline trace |
| U-024 | reg_pkg content | reg_pkg.svh (NOT_READ) | Register struct/type definitions | Read if register analysis needed |

## Identified Dead/Unreachable Code

| ID | Description | Evidence |
|----|-------------|----------|
| D-001 | `ifdef MEMC_DDR5_ONLY` blocks | cc_constants:129 (commented out), EN=0 |
| D-002 | `ifdef DDRCTL_LLC` blocks | cc_constants:107 (commented), EN=0 |
| D-003 | `ifdef DDRCTL_LPDDR` blocks | Not defined, license NotUsed |
| D-004 | CHB (CHI Bridge) code | Not defined, `DDRCTL_INCL_CHB` not active |
| D-005 | LPDDR4/LPDDR5 paths | License key NotUsed in header |
| D-006 | testbench mux modules | Only in simulation |

## Assumptions Made (with warnings)

| ID | Assumption | Risk |
|----|------------|------|
| A-001 | `ddrc_ddr4_mode=0` (DDR5 active) for analysis | Could be DDR4; needs runtime config |
| A-002 | Single-channel configuration | Could be dual-channel if UMCTL2_DUAL_CHANNEL=1 |
| A-003 | HIF bus connects arb_top to ddrc directly | Could go through XPI pipeline |
| A-004 | ts/gs/bsm is the primary scheduler path | Could be PAS path for DDR5 |

## Total Count

- HIGH priority: 6
- MEDIUM priority: 9
- LOW priority: 9
- Dead/Unreachable: 6
- Assumptions: 4
- **Total open items: 24**
