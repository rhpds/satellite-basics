# Module 09 — Enable the Tracer Service on RHEL Hosts

### Brief Overview

This module adds the Satellite Client 6 repository to the RHEL10 content view and installs the `katello-host-tools-tracer` package on the already-registered managed hosts via Satellite remote execution. The Tracer tool detects running services and applications that need a restart after RPM updates — a critical capability covered in module 10 (Update Errata). Because the managed hosts are already registered and their content view is published, adding the Satellite Client 6 repo requires publishing a new content view version and enabling repository access via an activation key override.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 07 (hosts registered to Satellite)
- **Estimated duration:** 20 minutes

### Learning Objectives

- Add the Satellite Client 6 repository to an existing content view and publish a new version
- Override repository access settings in an activation key to enable the Satellite Client 6 repository on managed hosts
- Install katello-host-tools-tracer on managed hosts using Satellite remote execution

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Add Satellite Client 6 repository to the RHEL10 content view | 5 min |
| 2 | Publish a new content view version | 4 min |
| 3 | Enable Satellite Client 6 access in the activation key | 4 min |
| 4 | Install Tracer on managed hosts via remote execution | 7 min |

### Detailed Steps

**Add the Satellite Client 6 Repository**

1. Navigate to **Content > Content Views** and open the **RHEL10** content view.
2. Click the **Repositories** tab.
3. Click **Add Repositories**.
4. Search for **Red Hat Satellite Client 6 for RHEL 10 x86_64 RPMs** and check its checkbox.
5. Click **Add Repositories** to confirm.

**Publish a New Version**

6. Navigate to the **Versions** tab and click **Publish New Version**.
7. Add a description such as `Added Satellite Client 6 repository`.
8. Click **Next**, review the summary, then click **Finish**.
9. Wait for the publish task to complete.
10. Promote the new version to the **Test** lifecycle environment.

**Enable Repository Access in the Activation Key**

11. Navigate to **Content > Activation Keys** and open the **RHEL10** activation key.
12. Click the **Repository Sets** tab.
13. Locate **Red Hat Satellite Client 6 for RHEL 10 x86_64 RPMs** in the list.
14. Change its override setting from **Default (Disabled)** to **Override to Enabled**.

**Install Tracer via Remote Execution**

15. Navigate to **Hosts > All Hosts** and select both `rhel1.lab` and `rhel2.lab`.
16. Click **Schedule Remote Job**.
17. In the **Job Category** dropdown, select **Commands**.
18. In the **Command** field, enter:
    ```bash
    dnf config-manager --set-enabled satellite-client-6-for-rhel-10-x86_64-rpms && dnf install -y katello-host-tools-tracer
    ```
19. Click **Submit** to run the job.
20. Navigate to **Monitor > Jobs** and confirm the job completes successfully on both hosts.
21. After the job finishes, navigate to **Hosts > All Hosts**, open `rhel1.lab`, and confirm the **Traces** tab is now visible and populated.

### Key Takeaways

- Adding a repository to a content view does not automatically make it available to already-registered hosts; a new content view version must be published and promoted.
- Activation key repository overrides allow enabling or disabling specific repositories without creating a new activation key.
- The Tracer tool (`katello-host-tools-tracer`) identifies processes using outdated libraries or binaries after RPM updates, enabling targeted service restarts instead of full reboots.

### Infrastructure Notes

- The Satellite Client 6 repository must be pre-synced in Satellite before this module; the lab setup automation handles this.
- Remote execution requires SSH connectivity from the Satellite smart proxy to the managed hosts — this is pre-configured in the lab environment.
- The `dnf config-manager` step is needed because the repository may be disabled in the host's yum configuration even after the activation key override; the override affects new registrations.
