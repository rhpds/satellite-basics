# Module 12 — Filter Content

### Brief Overview

This module demonstrates Satellite's content filtering capability by creating an exclude filter named "emacs" in the RHEL10 content view that blocks the `emacs` package family from being available to managed hosts. After configuring the filter, participants publish and promote a new content view version, then verify on `rhel1.lab` that `dnf install emacs` fails because the package is excluded from the content view. This shows how Satellite can enforce software governance by controlling exactly which packages are available in an environment.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 04 (RHEL10 content view exists and is promoted to Test)
- **Estimated duration:** 15 minutes

### Learning Objectives

- Create a content filter in Satellite to exclude specific packages from a content view
- Publish and promote a new content view version that includes the filter
- Verify that the filtered package is unavailable for installation on managed hosts

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create the emacs exclude filter | 5 min |
| 2 | Publish and promote a new content view version | 5 min |
| 3 | Test the filter on a managed host | 5 min |

### Detailed Steps

**Create the Filter**

1. Navigate to **Content > Content Views** and open the **RHEL10** content view.
2. Click the **Filters** tab.
3. Click **Create Filter**.
4. In the **Name** field, enter `emacs`.
5. Set **Content Type** to **RPM**.
6. Set **Filter Type** to **Exclude**.
7. Click **Save**.
8. On the filter detail page, click **Add Rule**.
9. In the **RPM Names** field, enter `emacs` (this matches all packages whose name starts with "emacs", including `emacs`, `emacs-common`, etc.).
10. Click **Save**.

**Publish and Promote a New Version**

11. Navigate to the **Versions** tab of the RHEL10 content view.
12. Click **Publish New Version**.
13. Add a description such as `Exclude emacs filter applied`.
14. Click **Next**, review the summary, then click **Finish**.
15. Wait for the publish task to complete.
16. Promote the new version to the **Test** lifecycle environment.

**Test the Filter**

17. Open a terminal on `rhel1.lab` (via the lab terminal tab or Satellite remote execution).
18. Attempt to install emacs:
    ```bash
    dnf install -y emacs
    ```
19. Confirm that the installation fails with a "No match for argument: emacs" or "Package not found" error.
20. This confirms that the content filter is correctly blocking the emacs package from being available in the Test environment.

### Key Takeaways

- Content filters allow administrators to control precisely which packages, errata, or module streams are available in a lifecycle environment, enabling software governance without modifying the upstream repositories.
- Exclude filters are most common — they block specific content while passing everything else through. Include filters do the inverse.
- A new content view version must be published and promoted for filter changes to take effect on managed hosts; this ensures changes are deliberate and auditable.

### Infrastructure Notes

- The emacs package is available in the RHEL 10 AppStream repository; the filter works because emacs is sourced from that repo, which is included in the RHEL10 content view.
- After this module, the emacs exclude filter remains active in the content view, which may affect subsequent modules if any require emacs (none do in this lab).
- The `dnf install -y emacs` command is the verification step; the error message confirms the filter is working.
