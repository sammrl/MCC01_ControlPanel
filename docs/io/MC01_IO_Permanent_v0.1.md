# MCC01 - Permanent Panel I/O

**Version:** v0.1
**Date:** 2026-04-26
**Status:** Draft

---

## Scope

 **permanent panel I/O** only. Spare embedded PLC
embedded terminals and open terminal blocks in the panel are intentionally reserved for
**field-demo cell wiring** — see [Demo / Field Reservation](#demo--field-reservation).
**Do not reassign reserved points without revising this document.**

## Hardware

- **PLC:** Allen-Bradley Micro850, P/N `2080-LC50-48QBB`
  - 28 embedded digital inputs (I-00 … I-27)
  - 20 embedded digital outputs (O-00 … O-19)
- **Programming software:** Connected Components Workbench (CCW) v21
- **Address format:** `_IO_EM_DI_xx` (embedded inputs), `_IO_EM_DO_xx` (embedded outputs)

## Power Architecture (context)

| PSU         | Part                | Role                                                                 |
|-------------|---------------------|----------------------------------------------------------------------|
| Control PSU | NVVV HDR-100-24     | Powers PLC, relays, indicators, control logic (24 VDC, 92 W)         |
| Load PSU    | AB 1606-XLP73       | Powers load circuits via WAGO 857-304 contact, gated by E-stop (24 VDC, 70 W) |
                                                        |

## Inputs (DI)

| Tag | Address         | Module    | Point | Description              | Field Device                          | Notes                                  |
|-----|-----------------|-----------|-------|--------------------------|---------------------------------------|----------------------------------------|
| I12 | `_IO_EM_DI_12`  | Embedded  | I-12  | Load PSU fault           | AB 1606-XLP73 DC-OK signal contact    | PLC logs fault if DC-OK drops          |
| I13 | `_IO_EM_DI_13`  | Embedded  | I-13  | Red pushbutton (op)      | 22 mm AB momentary PB — red           | Standard 22 mm AB plastic PB           |
| I14 | `_IO_EM_DI_14`  | Embedded  | I-14  | Green pushbutton (op)    | 22 mm AB momentary PB — green         | Standard 22 mm AB plastic PB           |
| I15 | `_IO_EM_DI_15`  | Embedded  | I-15  | Blue pushbutton (op)     | 22 mm AB momentary PB — blue          | Standard 22 mm AB plastic PB           |

## Outputs (DO)

| Tag | Address         | Module    | Point | Description       | Field Device                  | Notes                                       |
|-----|-----------------|-----------|-------|-------------------|-------------------------------|---------------------------------------------|
| O0  | `_IO_EM_DO_00`  | Embedded  | O-00  | Red indicator     | 22 mm AB 24 VDC LED — red     | Direct-driven from PLC (relay if isolation) |
| O1  | `_IO_EM_DO_01`  | Embedded  | O-01  | Green indicator   | 22 mm AB 24 VDC LED — green   | Direct-driven from PLC (relay if isolation) |
| O2  | `_IO_EM_DO_02`  | Embedded  | O-02  | Blue indicator    | 22 mm AB 24 VDC LED — blue    | Direct-driven from PLC (relay if isolation) |

## Hardwired Logic (non-PLC)

These devices are part of the panel but are **not PLC points**. They appear on
the schematic but won't show up in the PLC I/O list above.

| Tag      | Device                              | Function                                                                                         | Power Source                  |
|----------|-------------------------------------|--------------------------------------------------------------------------------------------------|-------------------------------|
| KM-LOAD  | WAGO 857-304 (24 VDC SPDT relay)    | Load-enable contactor: E-stop NC in series with coil; contact gates load PSU input              | 24 V control rail (NVVV)      |
| HL-LOAD  | Pilot lamp across load PSU output   | Visual indicator that load PSU output is live  | Load PSU output (1606-XLP73)  |
| ESTOP-1  | 22 mm E-stop, NC twist-release      | Master E-stop; NC contact in series with KM-LOAD coil                                            | 24 V control rail             |

## Demo / Field Reservation

The unused PLC terminals and open terminal blocks listed below are reserved for demo cell wiring.
### Reserved DI (Embedded)
***TBD***

### Reserved DO (Embedded)
***TBD***

### Reserved Terminals
All currently-unlanded signal and power terminal blocks on the DIN rail are
held for demo wiring. See panel layout drawing (TBD) for the physical map.

## Open Items

- [ ] Pick wire-numbering convention before populating wire numbers.
- [ ] Relocate HL-LOAD pilot lamp from internal DIN rail to panel face.

## Cross-references

- BOM: `docs/MC01_Master_BOM_v0.2.csv` / `.xlsx`
- I/O workbook (with reserve map): `docs/MC01_IO_List_v0.1.xlsx`

## Revision History

| Version | Date       | Author | Notes                                              |
|---------|------------|--------|----------------------------------------------------|
| v0.1    | 2026-04-26 | Sam    | Initial draft. 7 permanent points + 3 hardwired.   |
