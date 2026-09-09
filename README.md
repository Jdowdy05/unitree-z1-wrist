# Unitree Z1 wrist

A two-axis, 3D-printable wrist mechanism for the Unitree Z1, using four
ROBOTIS DYNAMIXEL XL330-M288-T servos. Two opposed servos drive each axis through
1:1 connections to their factory horns; there are no external gears or belts.

![Assembled wrist](docs/images/wrist.png)

**Prototype hardware:** check printed fits, cable clearance and operating loads
before use. No working payload or continuous-duty rating has been established.

## Start here

- **Print:** download the files in [stl/](stl/). Print one of each of the 18 files.
- **Edit in CAD:** open [cad/wrist.step](cad/wrist.step) in your CAD application,
  or [cad/wrist.FCStd](cad/wrist.FCStd) in FreeCAD.
- **Modify individual pieces:** use the named STEP files in [cad/parts/](cad/parts/).
- **Build:** follow the [assembly guide](docs/assembly.md) and [BOM](BOM.csv).
- **Download everything:** use [Download ZIP](https://github.com/Jdowdy05/unitree-z1-wrist/archive/refs/heads/main.zip),
  or clone this repository.

```sh
git clone https://github.com/Jdowdy05/unitree-z1-wrist.git
```

## Layout

```text
cad/
  wrist.FCStd           Native FreeCAD assembly, grouped by part type
  wrist.step            Complete assembly for other CAD applications
  parts/                18 individual printable-part STEP models
  source/
    Rebuild_Wrist.FCMacro
    dimensions.json     Main layout dimensions
  geometry.json         Export inventory, dimensions and mesh checks
stl/                    18 separate meshes in starting print orientations
docs/
  assembly.md           Assembly order, screw locations and print notes
  images/               Assembly and bearing-stack illustrations
BOM.csv                 Mechanical parts and purchased hardware
LICENSE
```

The assembly contains the wrist mechanism, a general-purpose recessed output
plate and nominal reference shapes for motors, bearings and M3 hardware.
The STL directory contains printable parts only. Purchased parts are not
included as printable meshes.

## Main dimensions

| Feature | Nominal value |
| --- | --- |
| Mechanism above the arm mounting face | 128 × 120 × 67 mm |
| Axis intersection / output-plate top | 50.5 mm above the arm mounting face |
| Intended travel | ±25° outer axis, ±20° inner axis |
| Output plate | 44 × 38 mm outline, 4 mm thick |
| General-purpose output pattern | Four Ø3.4 mm holes on a 28 × 14 mm rectangle |
| Nominal Z1 interface | Eight M3 positions on a Ø59.5 mm bolt circle |
| Support bearings | Four 6704 bearings, 20 × 27 × 4 mm |

The output plate's centre lies at the two intersecting axes. Points on an
attached tool away from that centre will move as the plate rotates. The stated
mechanism envelope excludes the screws' intended penetration into the arm.
Verify the actual arm flange and usable thread depth before installation.

## Parts to obtain

| Purchased item | Quantity |
| --- | ---: |
| XL330-M288-T servo, with factory horn | 4 |
| 6704 bearing, 20 mm bore × 27 mm OD × 4 mm wide | 4 |
| M3×8 socket-cap screw | 8 |
| M3×10 socket-cap screw | 12 |
| M3×12 socket-cap screw | 8 |
| M3×12 DIN7991, 90° countersunk screw with 6 mm head | 4 |
| Plain M3 nut, 5.5 mm across flats × 2.4 mm thick | 24 |
| ROBOTIS PHS M2×6 TAP horn screw | 16 |
| ROBOTIS PHS M2×8 TAP body screw | 16 |

These are installed quantities; obtain spares as needed. Check the servo
accessory bags before ordering tapping screws. Keep the factory horns and their
central retaining screws. The [BOM](BOM.csv) includes part-by-part use and sources.

Power, data wiring and a compatible TTL interface are separate from the
mechanical BOM. The XL330 uses 3.7–6.0 V, with 5 V recommended; the Z1's 24 V
supply must not connect directly to these servos. Use properly rated power
distribution and verify paired-motor directions, zero positions and current
sharing before powered operation. See [ROBOTIS documentation](https://emanual.robotis.com/docs/en/dxl/x/xl330-m288/).

## Printing

STLs are centred and placed at Z=0 in suggested starting orientations. They are
not G-code or a validated printer profile. Inspect supports for bearing roofs,
hub flanges, projecting shelves and horizontal holes before slicing. Retainers,
spacers and the output plate have functional flat-face orientations.

PETG is the starting material assumption. Calibrate bearing fits, journals,
nut pockets and screw holes on your printer. Layer direction, supports, walls,
creep and fastener preload affect the real assembly; a closed mesh does not
establish printed strength. Do not print the complete assembled STEP as one part.

## Editing the design

The FreeCAD document contains named solid features organised into printable
parts, purchased reference components and reference fasteners. It does not
contain a solved assembly constraint system or a full Sketcher history.

For reproducible changes, edit [cad/source/dimensions.json](cad/source/dimensions.json)
and the detailed geometry in [Rebuild_Wrist.FCMacro](cad/source/Rebuild_Wrist.FCMacro).
In FreeCAD, open **Macro → Macros**, select `cad/source/` as the macro location,
and run `Rebuild_Wrist`. It uses only standard FreeCAD modules and Python's
standard library, and rewrites the generated CAD and STL files in this repo.
Keep a copy or branch before rebuilding your modifications.

The JSON exposes main layout controls; detailed mounting features are fixed in
the macro. The generator checks connected solids and closed meshes. Changes
still require a new assembly, clearance and hardware-stack review.

## Verification and licence

The published default geometry has been checked as 26 valid component solids
and 18 closed STL meshes, with 56 nominal M3 hardware references. The unpowered
nominal mechanism is screened at 55 combinations of its two axis angles. These
checks do not cover arbitrary intermediate motion, real cables, printing,
load capacity or control behaviour.

Project-authored design files and CAD source are released under the [MIT licence](LICENSE).
Motor, bearing and fastener shapes are simple nominal reference envelopes;
manufacturer CAD is not redistributed here. Product names identify compatibility
and do not imply endorsement.
