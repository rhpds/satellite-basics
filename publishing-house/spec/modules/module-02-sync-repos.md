# Module 02 — Synchronize Repositories

### Brief Overview

This module documents the process of enabling and synchronizing RHEL 10 BaseOS and AppStream repositories from the Red Hat CDN inside Satellite. It is explicitly read-only: learners are instructed not to perform the synchronization steps because the repositories are pre-synchronized in the lab environment to avoid multi-hour wait times. The module exists to ensure participants understand the full Satellite workflow even when a time-consuming step is pre-done for them.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 01 (Satellite Web UI login)
- **Estimated duration:** 10 minutes

### Learning Objectives

- Identify the steps required to enable Red Hat repositories from the CDN in Satellite
- Describe the repository synchronization workflow and explain why pre-synchronization is used in this lab

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Navigate to Red Hat Repositories | 2 min |
| 2 | Review repository selection | 4 min |
| 3 | Review synchronization options (read-only) | 4 min |

### Detailed Steps

1. Navigate to **Content > Red Hat Repositories** in the Satellite Web UI.
2. Observe the repository selection interface where Red Hat CDN product repositories can be enabled by searching for the product and toggling repositories on.
3. Locate the **Red Hat Enterprise Linux 10 for x86_64 - BaseOS RPMs** and **Red Hat Enterprise Linux 10 for x86_64 - AppStream RPMs** entries — note these are already enabled in the lab environment.
4. Navigate to **Content > Sync Status** to view the synchronization status of all enabled repositories.
5. Observe that the RHEL 10 BaseOS and AppStream repositories show a "Synced" status — no action is needed.
6. **Do not** click the Sync Now button — repositories are already synchronized and re-synchronizing would cause unnecessary wait time.
7. Note the **Sync Plans** tab, which allows scheduling automatic recurring synchronizations; this is not configured in the lab but is relevant for production deployments.

### Key Takeaways

- Red Hat Satellite synchronizes content from the Red Hat CDN into an internal mirror, allowing disconnected or controlled content delivery to managed hosts.
- Synchronizing RHEL 10 repositories can take 30 minutes or more depending on network speed; the lab pre-syncs these to save time.
- Sync plans can automate recurring synchronizations on a schedule.

### Infrastructure Notes

- RHEL 10 BaseOS and AppStream repositories must be pre-synchronized before the lab begins; the setup automation handles this.
- The Satellite Client 6 repository is also pre-synced for use in module 09 (Tracer).
- No learner action is required; this module is documentation only.
