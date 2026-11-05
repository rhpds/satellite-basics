# Module 06 — Configure a Host Group

### Brief Overview

This module creates an "Application Servers" host group in Satellite and configures it to enforce a baseline system configuration using an Ansible role from RHEL System Roles. The firewall role (`rhel-system-roles.firewall`) is assigned with a JSON parameter that opens port 80/tcp, and the RHEL10 activation key is assigned to the group. Host groups allow Satellite to stamp consistent configuration on any host that joins the group, reducing per-host manual configuration.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 05 (RHEL10 activation key created)
- **Estimated duration:** 15 minutes

### Learning Objectives

- Create a host group in Satellite and associate it with a lifecycle environment, content view, and activation key
- Assign an Ansible role to a host group and configure role parameters using JSON
- Explain how host groups enforce consistent configuration across multiple managed hosts

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create the Application Servers host group | 4 min |
| 2 | Configure lifecycle environment and content view | 2 min |
| 3 | Assign the rhel-system-roles.firewall Ansible role | 4 min |
| 4 | Set the firewall role JSON parameter | 3 min |
| 5 | Assign the RHEL10 activation key | 2 min |

### Detailed Steps

1. Navigate to **Configure > Host Groups** in the Satellite Web UI.
2. Click **Create Host Group**.
3. In the **Name** field, enter `Application Servers`.
4. Under the **Host Group** tab, set:
   - **Lifecycle Environment:** Test
   - **Content View:** RHEL10
   - **Content Source:** satellite.lab (the internal Satellite capsule)
5. Click the **Activation Keys** tab and add `RHEL10` to the activation keys list.
6. Click **Save** to create the host group.
7. Navigate back to **Configure > Host Groups**, locate **Application Servers**, and click it to edit.
8. Click the **Ansible Roles** tab.
9. In the **Ansible Roles** search box, type `firewall` and select **rhel-system-roles.firewall** from the results.
10. Click the arrow to move the role to the **Selected** list.
11. Click **Submit** to save the role assignment.
12. Navigate to **Configure > Variables** (or the **Parameters** tab within the host group) to set the firewall role parameter.
13. Locate the `firewall` variable for `rhel-system-roles.firewall`.
14. Set the **Default Value** type to **Array** and enter the following JSON value:
    ```json
    [{"port":["80/tcp"],"state":"enabled"}]
    ```
15. Click **Submit** to save the parameter.

### Key Takeaways

- Host groups are templates that stamp lifecycle environment, content view, Ansible roles, and activation keys onto any host that joins the group, eliminating per-host manual configuration.
- RHEL System Roles ship with Satellite 6.19 and cover common configuration domains (firewall, SELinux, network, timesync, and more).
- Role parameters are passed as structured data (JSON) via Satellite's Smart Class Parameters or Host Group parameters, allowing flexible role customization without editing playbooks.

### Infrastructure Notes

- The `rhel-system-roles.firewall` Ansible role must be pre-imported into Satellite; this is typically done automatically when Satellite is installed with RHEL System Roles available.
- The JSON parameter `[{"port":["80/tcp"],"state":"enabled"}]` configures the firewall role to open port 80/tcp and enable the rule permanently.
- Ansible jobs run via Satellite's remote execution framework; SSH connectivity from `satellite.lab` to managed hosts must be established before the role runs.
