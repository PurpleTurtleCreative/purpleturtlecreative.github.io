---
title: Shortcodes
parent: Completionist
nav_order: 5
has_children: true
has_toc: false
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

Only "list" layout is displayed in the free version of Completionist. Additional layouts such as "calendar" are available to Completionist Pro users only.

**Attributes:**

- `src` – **Required.** The Asana project link.
  - When viewing a project in Asana, copy the URL in the web browser address bar (eg. `https://app.asana.com/0/1234567890/list`) or the URL from clicking "Copy project link" in the project's detail dropdown (eg. `https://app.asana.com/0/1234567890/1234567890`).
  - ⭐️ **Pro users** can display an Asana project in calendar layout by using the project's Calendar view link (eg. `https://app.asana.com/0/1234567890/calendar`) 
- `auth_user` – Optional. A WordPress user's ID to authenticate the Asana API requests.
  - By default, the *[Frontend Authentication User](/completionist/getting-started/#set-a-frontend-authentication-user)* saved in Completionist's settings is used.
  - The WordPress user must be connected to Asana via Completionist in wp-admin, or you may see a `401 Unauthorized` error on your website.
- `exclude_sections` – Optional. A comma-separated list of the names of the Asana project sections to exclude from display. Default "" (empty) to display all sections within the Asana project.
  - Note that HTML entities are encoded to keep compatibility with the WordPress Block Editor. For example, `exclude_sections="Design &amp; Development"` will exclude project sections named `Design & Development`.

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
- `show_tasks_attachments` – Optional. Set to "false" to hide tasks' additional attachments. Default "true".
  - Inline attachments in the tasks' descriptions will still be displayed if `show_tasks_description="true"`.
  - The following file extensions are supported:
    - Images: `jpg`, `jpeg`, `png`, `bmp`, `gif`
    - Videos: `mp4`
- `show_tasks_tags` – Optional. Set to "false" to hide tasks' tags. Default "true".
- `show_tasks_comments` – ⭐️ **Pro Only** Optional. Set to "true" to display tasks' comments. Default "false".

**Quick Copy (with default values):**

```
[ptc_asana_project src="<ASANA_PROJECT_URL>" auth_user="" exclude_sections="" show_name="true" show_description="true" show_status="true" show_modified="true" show_due="true" show_tasks_description="true" show_tasks_assignee="true" show_tasks_subtasks="true" show_tasks_completed="true" show_tasks_due="true" show_tasks_attachments="true" show_tasks_tags="true" show_tasks_comments="false"]
```

_**\*\*Remember** to change the `src` attribute value to the URL of the Asana project that you'd like to display!_


## [ptc_asana_project_list]

Displays a WordPress user's associated Asana projects' information and tasks.

<div class="banner banner-warning">
  <p>⭐️ This shortcode is available to <strong>Completionist Pro</strong> users only.</p>
</div>


**Attributes:**

This shortcode shares the same attributes as the singular `[ptc_asana_project]` shortcode plus the following:

- `layout` – Optional. The Asana project layout for all listed projects. Default 'list'.
  - Possible values are `list` and `calendar`
- `user` – Optional. A WordPress user's ID to determine which Asana projects to list. Defaults to the currently logged-in user.
  - See the "Asana Projects" setting in the WordPress user's profile to select which Asana projects the WordPress user is allowed to view.

**Quick Copy (with default values):**

```
[ptc_asana_project_list layout="list" user="" auth_user="" exclude_sections="" show_name="true" show_description="true" show_status="true" show_modified="true" show_due="true" show_tasks_description="true" show_tasks_assignee="true" show_tasks_subtasks="true" show_tasks_completed="true" show_tasks_due="true" show_tasks_attachments="true" show_tasks_tags="true" show_tasks_comments="false"]
```
