# Module 03 — Create a Lifecycle Environment

### Brief Overview

This module introduces the concept of application lifecycle environments in Red Hat Satellite and walks participants through creating a "Test" lifecycle environment path in the web UI. Lifecycle environments represent stages in the software promotion pipeline (for example: Library → Development → Testing → Production). Creating the "Test" environment here establishes the target stage that content views and activation keys reference in subsequent modules.

### Audience and Time

- **Audience:** Beginner Linux administrators completing the lab sequentially
- **Prerequisites for this module:** Module 02 (repositories synchronized)
- **Estimated duration:** 10 minutes

### Learning Objectives

- Explain the purpose of lifecycle environments in Satellite's content management model
- Create a "Test" lifecycle environment path in the Satellite Web UI

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Concept introduction — lifecycle environments | 3 min |
| 2 | Create the Test lifecycle environment | 7 min |

### Detailed Steps

1. Navigate to **Content > Lifecycle Environments** in the Satellite Web UI.
2. Observe the existing **Library** environment, which is the root of all lifecycle paths and receives synchronized content automatically.
3. Click **Create Environment Path**.
4. In the **Name** field, enter `Test`.
5. In the **Description** field, optionally enter a description such as `Test environment for RHEL 10 hosts`.
6. In the **Prior Environment** dropdown, select **Library** to place Test immediately after Library in the path.
7. Click **Save**.
8. Confirm that the new **Library → Test** path appears in the lifecycle environment list.

### Key Takeaways

- Lifecycle environments define a software promotion pipeline; content moves from Library through each stage as it is tested and approved.
- The Library environment always receives synchronized content first; additional environments receive promoted content views.
- The "Test" environment created here will be used as the target for content view promotion and activation key assignment in modules 04 and 05.

### Infrastructure Notes

- No special infrastructure requirements for this module; all steps are performed in the Satellite Web UI.
- The Library environment is created automatically by Satellite and cannot be deleted.
