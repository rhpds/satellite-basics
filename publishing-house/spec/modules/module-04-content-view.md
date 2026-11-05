# Module 04 — Create a Content View

### Brief Overview

This module walks participants through creating a "RHEL10" content view in Satellite that bundles the RHEL 10 BaseOS and AppStream repositories. After adding the repositories to the content view, participants publish the first version and promote it to the "Test" lifecycle environment created in module 03. Content views are the mechanism Satellite uses to deliver a curated, versioned snapshot of content to managed hosts.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 03 (Test lifecycle environment created)
- **Estimated duration:** 15 minutes

### Learning Objectives

- Create a content view in Satellite and add RPM repositories to it
- Publish a content view version and promote it to a target lifecycle environment

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create the RHEL10 content view | 4 min |
| 2 | Add BaseOS and AppStream repositories | 4 min |
| 3 | Publish the content view | 4 min |
| 4 | Promote to the Test environment | 3 min |

### Detailed Steps

1. Navigate to **Content > Content Views** in the Satellite Web UI.
2. Click **Create New View**.
3. In the **Name** field, enter `RHEL10`. The **Label** field auto-populates.
4. Leave the **Composite Content View** checkbox unchecked — this is a standard (non-composite) content view.
5. Click **Save**.
6. Click the **Repositories** tab within the content view.
7. Click **Add Repositories**.
8. In the repository list, locate **Red Hat Enterprise Linux 10 for x86_64 - BaseOS RPMs** and check its checkbox.
9. Locate **Red Hat Enterprise Linux 10 for x86_64 - AppStream RPMs** and check its checkbox.
10. Click **Add Repositories** to confirm.
11. Navigate to the **Versions** tab and click **Publish New Version**.
12. Optionally add a description such as `Initial publish with BaseOS and AppStream`.
13. Click **Next**, review the summary, then click **Finish**.
14. Wait for the publish task to complete (observe the status in the task notification bar).
15. Once published, locate **Version 1.0** in the versions list and click **Promote**.
16. Select the **Test** lifecycle environment and click **Promote Version**.
17. Confirm that Version 1.0 now shows the **Test** badge in the environments column.

### Key Takeaways

- Content views create a versioned, immutable snapshot of repository content; promoting a version to an environment makes that snapshot available to hosts in that environment.
- Hosts registered to the Test environment will only receive packages from the content view version currently promoted to Test.
- Publish and promote are separate operations — publishing creates a version in Library; promoting moves it into downstream environments.

### Infrastructure Notes

- Publish operations can take several minutes depending on repository size; the RHEL 10 repos in this lab are pre-synced, so publish is typically fast.
- No CLI commands are used in this module — all steps are via the Satellite Web UI.
