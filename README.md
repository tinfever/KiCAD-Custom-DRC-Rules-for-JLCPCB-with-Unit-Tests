# KiCAD Custom DRC Rules for JLCPCB with Unit Tests

- Supported only in KiCad 7
- Has to make some assumptions since not all JLCPCB rules make sense or they contradict each other
	- "PTH hole Size" has a minimum of 0.2mm. Makes no sense since min via size is clearly 0.15mm, and "Pad Size" indicates min PTH hole size is 0.5mm. Ignoring this rule. 
	- "Miniumum annular ring" of 0.13mm makes no sense. A standard 2-layer via of 0.3/0.5mm has an annular ring of 0.1mm which would be a violation if this was real. PTH have annular ring of 0.25mm specified in "Pad Size" section
	- 2oz copper "minimum annular ring" of 0.2mm is confusing because it isn't clear which other rules they are overriding with this.
	- In "Miniumum annular ring" section, PTH = 0.3mm makes no sense. Assuming they mean an actual hole size not total diameter including annular ring (unclear), vias can definitely go smaller than that. Again, "Pad Size" indicates min PTH hole size is 0.5mm.
	- Vias and PTH are the same thing with the same manufacturing process so having different rules for them is very confusing.


To use the rules in your project:
- Copy the contents of the "JLCPCB Rules Test.kicad_dru" file in to your Board Setup > Design Rules > Custom Rules section.
- Select your desired option from the "Minimum trace width and spacing" by uncommenting it. Confirm all others are commented. Options: 2-oz copper, 2-layer, or 4-layer
- Select your desired option from the "Via hole/diameter size" by uncommenting it. Confirm all others are commented. Options: 2-layer standard (0.3/0.5mm), 4-layer standard (0.3/0.45mm), 4-layer special (0.25/0.4mm), 4-layer special (0.2/0.35mm), or 4-layer special (0.15/0.3mm)
- Select your desired option from the "Board Outlines" by uncommenting it. Confirm all others are commented. Option: Default Edge Routing, or Special V-Score Clearance

!!Note: In KiCad you may still need to use Board Setup > Constraints > Minimum clearance to set your desired min. clearance, and then comment out all those rules in the custom rules section. KiCad will forcibly apply the custom rules min. clearance value even to netclasses with higher clearance values set. Thus making net class clearance rules useless especially for zones.
See here for more info: https://gitlab.com/kicad/code/kicad/-/issues/14490

To test/demo rules in included "JLCPCB Rule Test" PCB:
1) Open project in KiCad
2) Open Design Rules Checker
3) Make sure "Refill all zones before performing DRC" and "Report all errors for each track" are checked. Make sure "Test for parity between PCB and schematic" is unchecked.
4) Click "Run DRC"

Credit for the original rules that I debugged, tested, and added to:
- https://gist.github.com/denniskupec/e163d13b0a64c2044bd259f64659485e
- https://gist.github.com/darkxst/f713268e5469645425eed40115fb8b49

Misc notes:
- From "Drill Hole Size" in the JLCPCB rules, the minimum size of 0.15mm isn't tested because it is covered by the min via size, min PTH size, and min NPTH size rules.
- JLC specifies their via minimum size option with a preferred minimum and an actual minimum. Ex. 0.3mm/(0.4/0.45mm) means 0.3mm min hole in via, they'd prefer you use a min. via diameter 0.45mm but could go down to 0.4mm if really necessary. All of these rules use the "preferred" values.
- It isn't possible to have 0.127mm pad to pad (without hole) clearance to only apply to to pads without holes in Kicad, I think