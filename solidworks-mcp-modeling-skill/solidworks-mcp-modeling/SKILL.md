---
name: solidworks-mcp-modeling
description: Use when Codex needs to control SolidWorks through a local MCP or Python COM bridge for mechanical CAD modeling, drawing-to-3D reconstruction, staged part generation, STEP export, assembly previews, or diagnosing SolidWorks MCP failures. Especially useful for Chinese mechanical drawing contests, SolidWorks API workflows, fillet/chamfer safety, and avoiding destructive CAD automation.
---

# SolidWorks MCP Modeling

## Core Workflow

Use SolidWorks through MCP as a staged CAD automation workflow, not as blind command spam.

1. Inspect the drawing, existing CAD files, output folders, and MCP scripts before acting.
2. Connect to an already-open SolidWorks session unless the user explicitly wants one started.
3. Build or modify parts in stages: base geometry, cuts, local details, then fillets/chamfers.
4. Save intermediate files with stage names before overwriting final `SLDPRT`, `SLDASM`, `STEP`, or `DWG`.
5. Verify with SolidWorks file opens, bounding boxes, feature lists, and STEP reloads where possible.
6. Report exact files created and what remains approximate.

Read `references/workflow.md` when doing a multi-part or contest-modeling task. Read `references/api-capabilities.md` when deciding what current MCP tools can and cannot do.

## SolidWorks Safety Rules

- Do not apply global fillets or chamfers to complex castings.
- Add fillets/chamfers only after base bodies, holes, bosses, and cuts rebuild cleanly.
- Put large casting radii into sketches when possible; use edge fillets only for small, well-bounded edges.
- Treat failed fillets, RPC failures, or SolidWorks crashes as geometry/process signals, not as reasons to keep retrying the same call.
- Never overwrite the user's best working CAD file without first saving a timestamped or clearly named backup.
- If SolidWorks crashes, stop automation and ask the user to reopen the relevant file before continuing.

## Modeling Defaults

- Units: millimeters.
- Precision target: 0.01 mm when drawing dimensions are available.
- Output strategy: create stage files first, then final files.
- For unclear scanned dimensions, record assumptions instead of pretending they are drawing facts.
- For teaching/reference models, prioritize visible structure and stable rebuilds. For competition candidates, preserve a checklist of unverified dimensions and features.

## Typical File Names

Use descriptive stage names:

- `PartName_stage_01_base.SLDPRT`
- `PartName_stage_02_cuts.SLDPRT`
- `PartName_stage_03_edge_features.SLDPRT`
- `PartName_final_candidate.SLDPRT`
- `Assembly_preview.SLDASM`
- `Assembly_final_candidate.stp`

For contest tasks, create a short implementation note beside the CAD files describing which dimensions are confirmed, approximated, or pending.

## MCP Interaction Pattern

Prefer MCP tools when available:

- connect: `solidworks_connect`
- create documents: `sw_new_part`, `sw_new_assembly`
- sketch primitives: `sw_create_sketch`, `sw_draw_line`, `sw_draw_circle`, `sw_draw_polyline`
- features: `sw_extrude_sketch`, `sw_cut_extrude`, `sw_cut_hole`
- save/export: `sw_save_active`, `sw_export_active_step`
- assembly preview: `sw_insert_component`, `sw_zoom_to_fit`

If the MCP wrapper is missing a needed operation, use a local helper script only after explaining the purpose and keeping it scoped. Do not dump large scripts in the final answer unless the user explicitly asks for code.

## Verification

For every meaningful CAD deliverable, try to verify:

- SolidWorks document opens without crashing.
- Bounding box is plausible against the drawing.
- Key holes/cuts were reported as created.
- STEP file exists and has nontrivial size.
- Assembly contains expected components.
- Known limitations are written down.

Keep final responses brief: files changed, verification performed, remaining risks.
