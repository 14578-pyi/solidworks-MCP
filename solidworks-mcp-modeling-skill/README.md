# SolidWorks MCP Modeling Skill

Early preview Codex skill for controlling SolidWorks through a local MCP/Python COM bridge.

Skill folder:

```text
solidworks-mcp-modeling/
```

Upload this repository to GitHub, then install/use the `solidworks-mcp-modeling` skill folder in Codex.

This preview focuses on safe staged CAD automation:

- connect to SolidWorks MCP/COM bridge,
- build mechanical parts from drawings,
- save staged `SLDPRT`/`SLDASM`/`STEP` files,
- avoid unsafe global fillets/chamfers,
- recover from SolidWorks COM/RPC failures.

The skill does not include the MCP server implementation itself. It is a workflow and safety guide for agents using a SolidWorks MCP bridge.
