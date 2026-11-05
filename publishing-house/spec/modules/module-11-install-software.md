# Module 11 — Install Software

### Brief Overview

This module introduces Satellite host collections as a mechanism for grouping hosts and performing bulk software management operations. Participants create a "TMUX installation" host collection containing `rhel1.lab` and `rhel2.lab`, then install the `tmux` package on both hosts simultaneously using Satellite's Package Installation, Removal, and Update (PIRU) feature. The module demonstrates how Satellite centralizes software installation across multiple hosts without requiring direct SSH access to each one.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 07 (rhel1 and rhel2 registered to Satellite)
- **Estimated duration:** 15 minutes

### Learning Objectives

- Create a host collection in Satellite and add managed hosts to it
- Install a software package on multiple hosts simultaneously using Satellite's Package Installation feature
- Verify software installation on a managed host

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create the TMUX installation host collection | 4 min |
| 2 | Install tmux via the host collection | 7 min |
| 3 | Verify tmux installation on the host | 4 min |

### Detailed Steps

**Create the Host Collection**

1. Navigate to **Hosts > Host Collections** in the Satellite Web UI.
2. Click **Create Host Collection**.
3. In the **Name** field, enter `TMUX installation`.
4. Optionally add a description such as `Hosts for tmux bulk installation demo`.
5. Click **Save**.
6. Click the **Hosts** tab within the new host collection.
7. Click **Add Hosts**.
8. Select `rhel1.lab` and `rhel2.lab` from the host list.
9. Click **Add Selected** to add both hosts to the collection.

**Install tmux**

10. While still on the host collection detail page, click **Package Installation, Removal, and Update** (or navigate to the **Packages** tab).
11. In the **Package** field, enter `tmux`.
12. Select the **Install** operation.
13. Click **Submit** to schedule the installation job via remote execution.
14. Navigate to **Monitor > Jobs** and confirm the tmux installation completes successfully on both `rhel1.lab` and `rhel2.lab`.

**Verify Installation**

15. Open a terminal on `rhel1.lab` (or use Satellite's remote execution **Run Command** feature).
16. Run `tmux` to confirm the package is installed and launches correctly.
17. Exit tmux with `Ctrl+d` or by typing `exit`.

### Key Takeaways

- Host collections are persistent logical groups that simplify bulk operations; unlike one-off multi-host selections, collections are reusable.
- Satellite's Package Installation, Removal, and Update feature issues dnf commands across all hosts in a collection via remote execution.
- Host collections are also used for host-scoped content access overrides and reporting.

### Infrastructure Notes

- Remote execution must be functional for package installation to work via Satellite.
- `tmux` is available in the RHEL 10 AppStream repository, which is already in the RHEL10 content view promoted to the Test environment.
- No direct SSH to managed hosts is required for this module — all steps are via the Satellite Web UI.
