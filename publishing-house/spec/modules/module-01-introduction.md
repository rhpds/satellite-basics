# Module 01 — Introduction to Red Hat Satellite 6.19 Basics

### Brief Overview

This module orients the learner to the lab environment before any configuration work begins. It describes the topology — a Satellite 6.19 server (`satellite.lab`) paired with two RHEL 10 managed hosts (`rhel1.lab`, `rhel2.lab`) and an AI host (`rhel-ai.lab`) — and explains what participants will accomplish across the full lab. The module concludes with a guided login to the Satellite Web UI using provided admin credentials. It is the shortest module and is purely orientation with no hands-on configuration.

### Audience and Time

- **Audience:** Beginner Linux administrators or IT operations staff with basic SSH/terminal familiarity and no prior Satellite experience
- **Prerequisites for this module:** None — this is the first module
- **Estimated duration:** 10 minutes

### Learning Objectives

- Identify the lab environment topology, including the roles of `satellite.lab`, `rhel1.lab`, `rhel2.lab`, and `rhel-ai.lab`
- Navigate to the Satellite Web UI URL and log in with admin credentials

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Lab environment overview | 4 min |
| 2 | Log into the Satellite Web UI | 6 min |

### Detailed Steps

1. Review the lab topology diagram: `satellite.lab` (Satellite 6.19 server), `rhel1.lab` and `rhel2.lab` (RHEL 10 managed hosts), `rhel-ai.lab` (AI host running opencode + gpt-oss-120b).
2. Note that Satellite is pre-installed and the RHEL 10 repositories are already synchronized — no initial setup is required.
3. Open a browser tab and navigate to the Satellite Web UI URL provided in the lab environment (typically `https://satellite.lab`).
4. Enter the admin username and password from the lab credentials panel.
5. Confirm that the Satellite dashboard loads, showing the Overview page with zero managed hosts.
6. Briefly explore the navigation menu to identify the key areas used in later modules: Content, Hosts, Configure, and Insights.

### Key Takeaways

- Red Hat Satellite 6.19 is a lifecycle management server that centralizes content, configuration, and compliance for RHEL hosts.
- The lab provides a fully pre-installed Satellite environment so participants can focus on configuration rather than installation.
- The Satellite Web UI is the primary interface for most tasks in this lab; the hammer CLI is used in one module.

### Infrastructure Notes

- `satellite.lab` has Satellite 6.19 installed and running; no additional provisioning is needed for this module.
- Admin credentials are injected by the lab environment provisioning system and displayed in the learner's lab panel.
