# MC-01 Panel — Power Distribution

## Overview

The MC-01 panel uses a three-rail power architecture: a 24V control rail (CPU,
networking infrastructure), a 24V load rail (actuators, output stages, indicator
lamps), and a 5V rail (Pi 5, router). Control and load rails are separately
sourced and protected so a load-side fault cannot disable the PLC's CPU or
network communications.

##TODO
- [ ] Add annotations
- [ ] Add earth ground path from AC mains entry
- [ ] Add legend (color = rail, line weight, dashed = future)
- [ ] Add Design Decisions callout box on canvas (or rely on README for these)
- [ ] Confirm PSU model numbers and update labels
- [ ] create grounding diagram
