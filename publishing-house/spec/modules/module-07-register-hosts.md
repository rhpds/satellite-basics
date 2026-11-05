# Module 07 — Register Hosts

### Brief Overview

This module uses the hammer CLI from the `satellite.lab` terminal to generate a global registration script, then registers `rhel1.lab` and `rhel2.lab` with Satellite via SSH. After registration, participants verify that both hosts appear in the Satellite Web UI under the "Application Servers" host group and confirm that the managed host's yum repository configuration points to the Satellite server instead of the Red Hat CDN. This is the first module with significant CLI interaction.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 06 (Application Servers host group configured with RHEL10 activation key)
- **Estimated duration:** 15 minutes

### Learning Objectives

- Generate a global registration command using the hammer CLI on `satellite.lab`
- Register RHEL 10 hosts to Satellite using an SSH-delivered registration script
- Verify host registration in the Satellite Web UI and confirm repository configuration on the managed host

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Generate the registration command with hammer | 5 min |
| 2 | Register rhel1 and rhel2 via SSH | 6 min |
| 3 | Verify registration in the Web UI and on the host | 4 min |

### Detailed Steps

1. Open a terminal session on `satellite.lab` (use the Satellite terminal tab in the lab environment).
2. Run the following hammer command to generate a global registration script for the "Application Servers" host group:
   ```bash
   hammer host-registration generate-command \
     --hostgroup "Application Servers" \
     --insecure 1 \
     --setup-insights 1 \
     --force 1
   ```
3. The command outputs a `curl | bash` registration script. Copy the script to the clipboard or store it in a shell variable:
   ```bash
   export REGISTRATION_SCRIPT=$(hammer host-registration generate-command \
     --hostgroup "Application Servers" \
     --insecure 1 \
     --setup-insights 1 \
     --force 1)
   ```
4. Register `rhel1.lab` by piping the script over SSH:
   ```bash
   ssh -o StrictHostKeyChecking=no root@rhel1 $REGISTRATION_SCRIPT
   ```
5. Wait for the registration to complete and confirm a success message is returned.
6. Register `rhel2.lab` using the same script:
   ```bash
   ssh -o StrictHostKeyChecking=no root@rhel2 $REGISTRATION_SCRIPT
   ```
7. Navigate to **Hosts > All Hosts** in the Satellite Web UI.
8. Confirm that `rhel1.lab` and `rhel2.lab` appear in the list, associated with the **Application Servers** host group and the **Test** lifecycle environment.
9. On `rhel1.lab` (or via the terminal), verify the repository configuration:
   ```bash
   cat /etc/yum.repos.d/redhat.repo
   ```
10. Confirm that the `baseurl` entries point to `satellite.lab` (not `cdn.redhat.com`), confirming the host is consuming content from Satellite.

### Key Takeaways

- The `hammer host-registration generate-command` creates a reusable registration script that embeds the host group, activation key, and Satellite server details.
- The `--insecure 1` flag is used in lab environments where the Satellite TLS certificate is self-signed; production environments should use a trusted certificate.
- After registration, managed hosts fetch all RPM content from the Satellite server's internal mirror, not directly from the Red Hat CDN.

### Infrastructure Notes

- SSH root access from `satellite.lab` to `rhel1.lab` and `rhel2.lab` must be pre-configured in the lab environment (passwordless SSH key or SSH agent forwarding).
- The `--setup-insights 1` flag configures the Insights client on the host, which is used in module 08.
- The `--force 1` flag re-registers hosts that may have been previously registered; safe to use in lab resets.
