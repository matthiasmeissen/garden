# PCB Pre-Fabrication Review

[tags: #pcb #electronics #eurorack]

Checks to run before sending a board to fab. DRC catches a lot, but the items below are the ones DRC cannot see — or can see but silently tolerates. Worth walking through every time.

## 1:1 Print Footprint Check

Print the board at true scale and physically hold each component over the paper. This is the single most reliable way to catch hole-size and pad-spacing errors — the category that produces "board comes back and the parts don't fit". DRC will not help here. Keep a copy of the printout as the last-checkpoint artefact before upload.

## Net-by-Net Highlighter Method

Print the schematic, then go through each net on the board and highlight it on the schematic as confirmed. When every net on the schematic is highlighted, nothing has been missed. This is the manual equivalent of automated netlist-vs-layout checking when the tool chain doesn't provide it.

## Copper Pour: Only Pour Where Ground Lives

If all GND routing is on the top layer, a top-layer GND pour is sufficient — do not add a bottom-layer pour with vias that serve no purpose. After pouring, scan the result for **isolated copper islands** (dead copper) the pour created but did not connect to GND. Dead copper is either wasted or — if it accidentally couples signal — a problem.

## Thermal Relief on GND Pads

A pad solidly connected to a large copper pour becomes a heat sink and makes hand-soldering miserable. EasyEDA defaults to thermal relief (spoke pattern on GND pad connections), which is correct for hand assembly. Override to a solid connection only where current demands it.

## Resistor Placement in a Series LED Circuit

Electrically indifferent — the same current flows through every element in a series loop. Convention is **high-side** (between positive rail and anode) for schematic readability, but the circuit behaves identically either way. Put it wherever the layout is cleanest; don't agonise.

## EasyEDA to PCBWay Workflow

Export Gerber from EasyEDA — produces a ZIP containing copper, mask, silkscreen, outline, and drill files. Upload the ZIP directly to PCBWay's instant quote page; their system auto-detects dimensions and layer count. The rendered preview is the last checkpoint — visually verify it matches expectations before clicking order. Optionally open the Gerber ZIP in an independent viewer (PCBWay's, or `gerbview`) for a second pair of eyes.

## See Also

- [[electronics|Electronics]]
