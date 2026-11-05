# Module 05 — Create an Activation Key

### Brief Overview

This module guides participants through creating a "RHEL10" activation key in Satellite and linking it to the Test lifecycle environment and the RHEL10 content view. Activation keys bundle subscription and content access settings so that host registration is fully automated — a host that registers using the key automatically attaches the correct subscriptions and gains access to the correct repositories without manual intervention.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 04 (RHEL10 content view published and promoted to Test)
- **Estimated duration:** 10 minutes

### Learning Objectives

- Create an activation key in Satellite and configure its lifecycle environment and content view associations
- Explain how activation keys automate subscription attachment and content access during host registration

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create the RHEL10 activation key | 6 min |
| 2 | Review key configuration | 4 min |

### Detailed Steps

1. Navigate to **Content > Activation Keys** in the Satellite Web UI.
2. Click **Create Activation Key**.
3. In the **Name** field, enter `RHEL10`.
4. In the **Environment** dropdown, select **Test**.
5. In the **Content View** dropdown, select **RHEL10**.
6. Click **Save**.
7. On the activation key detail page, click the **Subscriptions** tab and confirm that the appropriate subscriptions are attached (or verify the key inherits subscriptions from the organization's Simple Content Access settings).
8. Click the **Repository Sets** tab to review which repositories the key grants access to — BaseOS and AppStream should be listed.
9. Note the activation key name `RHEL10`; this will be referenced in the host group configuration (module 06) and the host registration command (module 07).

### Key Takeaways

- Activation keys eliminate manual subscription attachment during host registration by pre-configuring environment, content view, and subscription settings.
- A single activation key can be reused for all hosts that share the same lifecycle environment and content requirements.
- The key created here (`RHEL10`) is associated with the Test environment and RHEL10 content view, ensuring registered hosts receive only the content promoted to that environment.

### Infrastructure Notes

- No CLI commands are used in this module; all steps are via the Satellite Web UI.
- If Simple Content Access (SCA) is enabled on the Satellite organization (the default for new Satellite 6.19 installations), explicit subscription attachment may not be required.
