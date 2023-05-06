# KiCAD Custom DRC Rules for JLCPCB with Unit Tests

- Supported only in KiCad 7
- Has to make some assumptions since not all JLCPCB rules make sense or they contradict each other

To use the rules in your project:
- Copy the contents of the "JLCPCB Rules Test.kicad_dru" file in to the Board Setup > Design Rules > Custom Rules section.

To test/demo rules in included "JLCPCB Rule Test" PCB:
1) Open project in KiCad
2) Open Design Rules Checker
3) Make sure "Refill all zones before performing DRC" and "Report all errors for each track" are checked. Make sure "Test for parity between PCB and schematic" is unchecked.
4) Click "Run DRC"

Credit for the original rules that I debugged, tested, and added to:
- https://gist.github.com/denniskupec/e163d13b0a64c2044bd259f64659485e
- https://gist.github.com/darkxst/f713268e5469645425eed40115fb8b49
