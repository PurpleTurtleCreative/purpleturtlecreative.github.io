---
title: Shortcodes
parent: Completionist
nav_order: 5
---

# Shortcodes
{: .no_toc }

Display Asana tasks on your website to improve work transparency and collaboration—while reducing users within your Asana workspace.
{: .text-beta .fw-300 .text-grey-dk-000}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## [ptc_asana_project]

Displays Asana project information and tasks.

Only the "list" layout is currently used, but support for the "board" layout is planned to also be implemented.

**Attributes:**

- `src` – **Required.** The Asana project link.
  - When viewing a project in Asana, copy the URL in the web browser address bar (eg. `https://app.asana.com/0/1234567890/list`) or the URL from clicking "Copy project link" in the project's detail dropdown (eg. `https://app.asana.com/0/1234567890/1234567890`).
- `auth_user` – Optional. A WordPress user's ID to authenticate the Asana API requests.
  - By default, the *[Frontend Authentication User](/completionist/getting-started/#set-a-frontend-authentication-user)* saved in Completionist's settings is used.
  - The WordPress user must be connected to Asana via Completionist in wp-admin, or you may see a `401 Unauthorized` error on your website.
- `show_name` – Optional. Set to "false" to hide the project's name. Default "true".
- `show_description` – Optional. Set to "false" to hide the project's description. Default "true".
- `show_status` – Optional. Set to "false" to hide the project's current status update and completion status. Default "true".
- `show_modified` – Optional. Set to "false" to hide the project's last modified date and time. Default "true".
- `show_due` – Optional. Set to "false" to hide the project's due date. Default "true".
- `show_tasks_description` – Optional. Set to "false" to hide tasks' descriptions. Default "true".
- `show_tasks_assignee` – Optional. Set to "false" to hide tasks' assignee. Default "true".
- `show_tasks_subtasks` – Optional. Set to "false" to hide tasks' subtasks. Default "true".
  - Note that only the immediate subtasks are ever displayed. Subtasks of subtasks are never displayed.
- `show_tasks_completed` – Optional. Set to "false" to hide completed tasks. Default "true".
  - If enabled, completed tasks will be shown (if any) and all "checkmark bubbles" will be displayed.
  - This setting also applies to subtasks.
- `show_tasks_due` – Optional. Set to "false" to hide tasks' due dates. Default "true".

**Quick Copy:**

```
[ptc_asana_project src="" auth_user="" show_name="true" show_description="true" show_status="true" show_modified="true" show_due="true" show_tasks_description="true" show_tasks_assignee="true" show_tasks_subtasks="true" show_tasks_completed="true" show_tasks_due="true"]
```

*Remember to set the `src` attribute to the URL of the Asana project that you'd like to display!*
