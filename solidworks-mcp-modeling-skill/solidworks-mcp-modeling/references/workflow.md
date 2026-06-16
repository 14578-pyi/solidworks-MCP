# SolidWorks MCP CAD Workflow

## Drawing-to-3D Process

1. Extract part list, drawing pages, and target filenames.
2. Build a dimension ledger before modeling complex parts.
3. Create stable base solids first:
   - revolved/cylindrical parts before castings,
   - simple pads before complex arms,
   - holes and cuts after base bodies.
4. For castings:
   - large visible radii belong in sketches or local pad profiles,
   - small edge blends can be post-feature fillets only when local geometry allows,
   - never use global all-edge fillets on a contest casting.
5. Save after every stable phase.
6. Assemble with coarse coordinates first; add mates only when the MCP/API has stable support.
7. Export STEP only after the native file saves successfully.

## Fillet and Chamfer Procedure

Use this order:

1. Finish base body and all cuts.
2. Rebuild and save a pre-edge-feature backup.
3. Add large sketch radii while creating the profile, not afterward.
4. Add small edge fillets one group at a time.
5. Add C1 chamfers last.
6. Rebuild and save after each group.

Reject a fillet target if:

- the edge is shorter than the needed radius space,
- adjacent faces are missing or fragmented,
- the radius would eat through a nearby hole or boss,
- the model already has a conflicting blend.

## Assembly Procedure

1. Insert the frame/base component first.
2. Insert shaft/support/disc along the main axis.
3. Insert arms, knobs, pads, pins, spacers, and bracket.
4. Use coordinate placement for preview assemblies.
5. Use mates only when there is a tested MCP/API wrapper for the required mate type.
6. Save native assembly and STEP as separate deliverables.

## Crash Recovery

If SolidWorks crashes or COM reports RPC failure:

1. Stop automation immediately.
2. Ask the user to reopen SolidWorks and the latest candidate file.
3. Run a read-only active-document check before continuing.
4. Continue from the latest verified stage file, not from memory.
