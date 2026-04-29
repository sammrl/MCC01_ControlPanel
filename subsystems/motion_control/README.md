## Motion Control — AXIS_1

### Hardware

| Component | Details |
|-----------|---------|
| PLC | AB Micro850 2080-LC50-48QBB |
| PTO Channel | EM_0 — Pulse: DO_00, Direction: DO_03 |
| Driver | TB6600 4A 9-42V — 1600 pulses/rev, 1.5A current setting |
| Motor | NEMA 17 17HS19-2004S1 — 12V, 2A, 200 RPM |

### Wiring Notes

- 2kΩ current-limiting resistors on PUL+ and DIR+ (24V PLC output → 5V opto input)
- PUL− and DIR− tied to load PSU 0V common
- ENA left unconnected (driver internally enabled)
- Load PSU V+ confirmed landed on output group COM terminal

### Control Logic

- 3-position selector switch drives Execute inputs directly on motion blocks
- MC_MoveVelocity: rising edge starts continuous motion
- MC_Halt: rising edge decelerates to standstill
- No XIC contacts on motion rungs — Execute pins driven directly by input variables

### Status

Working — start/stop via 3-position selector switch
