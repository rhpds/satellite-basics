# Module 13 — Satellite AI Integration

### Brief Overview

This module demonstrates Red Hat Satellite's Model Context Protocol (MCP) server integration, which enables an AI assistant to query and act on Satellite data using natural language. Participants use the `opencode` TUI (or its web GUI equivalent) on `rhel-ai.lab` — which runs the minimax-m2 LLM — to issue natural language prompts that query the Satellite inventory, discover hosts with pending errata, and trigger remote execution patching jobs. This module requires no prior AI experience; it shows how existing Satellite capabilities are exposed through an AI interface.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 07 (hosts registered to Satellite with known errata state)
- **Estimated duration:** 20 minutes

### Learning Objectives

- Launch the opencode AI client on `rhel-ai.lab` and connect it to the Satellite MCP server
- Query Satellite inventory data using natural language prompts via the opencode TUI
- Trigger a Satellite remote execution patching job using a natural language instruction to the AI assistant

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Introduction — Satellite MCP server and opencode | 3 min |
| 2 | Launch opencode and verify Satellite MCP connection | 4 min |
| 3 | Query inventory using natural language | 6 min |
| 4 | Discover hosts with pending errata via AI | 4 min |
| 5 | Trigger remote execution patching via AI | 3 min |

### Detailed Steps

**Introduction**

1. Review the concept: the Satellite MCP server exposes Satellite API capabilities as MCP tools that any MCP-compatible AI client can call. The `opencode` TUI on `rhel-ai.lab` is configured with the minimax-m2 model and the Satellite MCP server endpoint.

**Launch opencode**

2. Open a terminal session on `rhel-ai.lab` (use the rhel-ai terminal tab in the lab environment).
3. Launch the opencode TUI:
   ```bash
   opencode
   ```
4. Confirm that opencode starts and shows the minimax-m2 model is active.
5. Verify the Satellite MCP server is connected — look for a "satellite" tool listed in the available tools panel (or run `/tools` in the opencode TUI).

**Query Inventory**

6. At the opencode prompt, type the following natural language query and press Enter:
   > What is the total number of hosts in the Satellite inventory?
7. Observe that opencode calls the Satellite MCP tool, retrieves the host count, and displays the result.
8. Submit a follow-up query:
   > List the names of all hosts registered to Satellite.
9. Confirm that `rhel1.lab` and `rhel2.lab` appear in the response.

**Discover Hosts with Pending Errata**

10. Submit the following query:
    > Which hosts have pending errata that have not been applied yet?
11. Review the response — opencode queries the Satellite API for errata applicability and returns hosts with outstanding errata.

**Trigger Remote Execution via AI**

12. Submit the following instruction:
    > Trigger a remote execution job to apply all pending errata to rhel1.
13. Observe that opencode invokes the Satellite MCP tool to create a remote execution job targeting `rhel1.lab`.
14. Navigate to **Monitor > Jobs** in the Satellite Web UI to confirm the remote execution job was created and is running.

### Key Takeaways

- The Satellite MCP server translates Satellite API operations into MCP tools that AI clients can call, enabling natural language control of Satellite without custom scripting.
- The minimax-m2 model (open-source, running locally on `rhel-ai.lab`) handles language understanding; it does not send any Satellite data to an external service.
- AI-driven operations still run through Satellite's existing RBAC and job execution infrastructure — the AI is an interface layer, not a bypass.

### Infrastructure Notes

- `rhel-ai.lab` must have opencode installed, the minimax-m2 model pre-loaded, and the Satellite MCP server endpoint configured — this is handled by the lab setup automation.
- The Satellite MCP server must be enabled in Satellite settings and configured with appropriate API credentials for the opencode client to authenticate.
- This module uses the minimax-m2 open-source LLM, which requires the `rhel-ai.lab` VM to have sufficient RAM to load the model (sizing TBD in infrastructure phase).
- No GPU is required — minimax-m2 runs in CPU inference mode in this lab (MaaS pattern).
