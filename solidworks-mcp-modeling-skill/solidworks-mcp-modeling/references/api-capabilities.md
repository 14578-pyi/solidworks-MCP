# Current SolidWorks MCP Capabilities

This reference describes the early MCP bridge capabilities observed in the local `solidworks_mcp` project.

## Stable or Partly Verified

- Connect to a running SolidWorks session.
- Create a new part or assembly document.
- Start and close sketches on standard planes.
- Draw lines, circles, rectangles, polygons, and polylines.
- Extrude active/latest sketches.
- Create cylinders/discs/shaft-like solids.
- Cut circular holes and cut active sketches.
- Create repeated circular hole patterns by drawing many circles in one sketch.
- Save native SolidWorks documents.
- Export/save STEP files.
- Insert components into an assembly by coordinates.
- Zoom to fit.
- List feature tree entries for debugging.

## Known Risky Areas

- Global fillet/chamfer calls are unsafe for complex parts.
- Selected-edge fillets require careful edge identification and may fail due to geometry limits.
- SolidWorks COM can expose methods as properties in some environments.
- `OpenDoc6` may need byref error/warning arguments depending on COM binding state.
- SolidWorks RPC failures often mean the app crashed, is busy, or has a modal dialog.
- Current assembly support is mostly coordinate insertion, not robust mate creation.

## Missing or Not Yet Stable

- Robust selected-edge/face naming.
- Sketch constraints and dimensions.
- Mate creation wrappers for concentric, coincident, distance, and angle mates.
- Toolbox standard part insertion.
- Drawings, BOMs, balloons, and DWG export.
- Reliable scan/loft/sweep/mirror feature wrappers.
- Automated interference detection wrappers.

## Practical Rule

Use MCP for stable primitives and staged automation. Use local helper scripts for carefully scoped operations that are not yet exposed as MCP tools, then fold stable patterns back into MCP later.
