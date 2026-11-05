# Module 10 — Update Errata

### Brief Overview

This module demonstrates Satellite's errata management capabilities. Participants filter the errata list to show installable errata for the managed hosts, apply selected errata to `rhel1.lab` and `rhel2.lab` through Satellite remote execution, and then use the Tracer tab to restart any services that were updated and require a restart. This module directly builds on the Tracer installation from module 09 and shows the full errata remediation cycle.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 09 (katello-host-tools-tracer installed on managed hosts)
- **Estimated duration:** 15 minutes

### Learning Objectives

- Filter the errata list in Satellite to identify installable errata for managed hosts
- Apply selected errata to multiple hosts simultaneously using Satellite remote execution
- Use the Traces tab to identify and restart services affected by package updates

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Filter and review installable errata | 4 min |
| 2 | Apply errata to rhel1 and rhel2 | 6 min |
| 3 | Resolve Traces — restart affected services | 5 min |

### Detailed Steps

**Apply Errata**

1. Navigate to **Content > Errata** in the Satellite Web UI.
2. In the **Applicability** filter, select **Applicable** to show only errata that apply to registered hosts.
3. Review the list; note errata types (security, bugfix, enhancement) and their severity ratings.
4. Select one or more errata entries (or select all applicable errata).
5. Click **Apply to Hosts**.
6. In the host selection dialog, choose both `rhel1.lab` and `rhel2.lab`.
7. Review the job template that will be used (typically the **Katello Errata - Install** template).
8. Click **Submit** to schedule the remote execution job.
9. Navigate to **Monitor > Jobs** and observe the job progress on both hosts.
10. Wait for the job to complete and confirm a success status.

**Resolve Traces**

11. Navigate to **Hosts > All Hosts** and open `rhel1.lab`.
12. Click the **Traces** tab.
13. Review the list of services or processes that require a restart after the package updates.
14. Select all traces and click **Restart via Remote Execution** (or the equivalent action).
15. Navigate to **Monitor > Jobs** to confirm the restart job completes successfully.
16. Repeat the trace resolution for `rhel2.lab`.
17. Navigate back to the **Traces** tab on each host and confirm the trace list is now empty.

### Key Takeaways

- Satellite's errata management allows targeted patch application to individual hosts or host groups without needing to log into each host manually.
- The Tracer tab identifies processes using outdated shared libraries after a package update, enabling surgical service restarts rather than requiring a full system reboot.
- Errata can be filtered by type (security, bugfix, enhancement) and severity (critical, important, moderate, low) to prioritize remediation efforts.

### Infrastructure Notes

- All steps in this module are performed through the Satellite Web UI; no direct CLI access to managed hosts is required.
- Remote execution (REX) must be functional for errata application — SSH connectivity from the Satellite smart proxy to managed hosts must be working.
- Tracer requires that hosts have Satellite's katello-agent or use REX-based communication; the lab uses REX.
