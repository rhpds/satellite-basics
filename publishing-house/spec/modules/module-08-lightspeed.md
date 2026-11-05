# Module 08 — Red Hat Lightspeed for Satellite

### Brief Overview

This module explores Red Hat Lightspeed services integrated with Satellite 6.19 in a disconnected lab environment. It covers two Lightspeed features: the Advisor service (which surfaces insights-client recommendations and allows one-click remediation via auto-generated Ansible playbooks) and the Vulnerability service (a tech-preview feature that requires downloading a CVE map XML file from security.access.redhat.com and placing it on the Satellite server). This is the most content-rich module and introduces participants to AI-assisted operations within Satellite.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 07 (rhel1 and rhel2 registered with Insights client enabled)
- **Estimated duration:** 20 minutes

### Learning Objectives

- Review Red Hat Lightspeed Advisor recommendations for managed hosts and apply remediations using auto-generated Ansible playbooks
- Configure the Lightspeed Vulnerability service by downloading and placing the CVE map file on the Satellite server
- Demonstrate the Vulnerability service by reviewing CVE exposure for managed hosts and disabling analysis for a specific host

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Review Lightspeed Advisor recommendations | 6 min |
| 2 | Apply advisor recommendations via Ansible playbook | 5 min |
| 3 | Download and configure the CVE map for Vulnerability | 5 min |
| 4 | Review vulnerability data and disable analysis for a host | 4 min |

### Detailed Steps

**Advisor Recommendations**

1. Navigate to **Insights > Advisor > Recommendations** in the Satellite Web UI.
2. Review the list of advisor recommendations for `rhel1.lab` and `rhel2.lab`.
3. Select one or more recommendations with available remediations.
4. Click **Remediate** to open the remediation wizard.
5. Review the auto-generated Ansible playbook that Satellite will run to address the selected recommendations.
6. Click **Execute Playbook** (or the equivalent button) to run the remediation via Satellite remote execution.
7. Navigate to **Monitor > Jobs** to watch the job run and confirm it completes successfully.

**Vulnerability Service (Tech Preview)**

8. On `satellite.lab`, download the CVE map XML file from the Red Hat security API:
   ```bash
   curl -o cvemap.xml https://security.access.redhat.com/data/meta/v1/cvemap.xml
   ```
9. Copy the downloaded file to the Foreman data directory:
   ```bash
   cp cvemap.xml /var/lib/foreman/
   ```
10. Navigate to **Insights > Vulnerability** in the Satellite Web UI.
11. Confirm that CVE data is now populated for the managed hosts.
12. Review the list of CVEs and their severity ratings.
13. To disable vulnerability analysis for a specific host, navigate to the host detail page, locate the Vulnerability section, and toggle the **Disable vulnerability analysis** option.

### Key Takeaways

- Red Hat Lightspeed Advisor surfaces insights-client recommendations and enables one-click remediation without manually writing Ansible playbooks.
- The Vulnerability service requires a local CVE map file in disconnected environments because it cannot reach the Red Hat security API from managed hosts.
- The Vulnerability service is a tech-preview feature in Satellite 6.19 — it may change or have limitations not present in GA features.
- Disabling vulnerability analysis for a host excludes it from CVE reporting, which can be useful for hosts in controlled environments where known CVEs are accepted.

### Infrastructure Notes

- The `insights-client` must be installed and registered on `rhel1.lab` and `rhel2.lab` (handled by the `--setup-insights 1` flag in module 07).
- The CVE map download requires outbound internet access from `satellite.lab` to `security.access.redhat.com` — this is listed as an external service dependency for the lab.
- The Vulnerability service tech-preview status means it must be explicitly enabled in Satellite settings before it appears in the Insights menu.
