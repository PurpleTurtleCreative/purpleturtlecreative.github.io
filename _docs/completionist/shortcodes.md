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

<div class="banner banner-warning">
  <p><strong>This page contains custom code snippets.</strong></p>
  <p>Please seek a WordPress developer for guidance if you're not familiar with adding custom code to WordPress websites!</p>
</div>


## Caching

**Frontend requests are cached by default for 15 minutes.** This improves website performance by reducing the frequency that data is requested from Asana.

### Changing the cache TTL

If you find that Asana data is not being updated often enough, you may implement the following filter hook.

This reduces the cache duration to 5 minutes:

```php
add_filter( 'ptc_completionist_request_tokens_ttl', 'ptc_get_request_tokens_ttl', 10, 1 );
function ptc_get_request_tokens_ttl( $ttl ) {
  return 5 * MINUTE_IN_SECONDS;
}
```

You may also increase the cache duration, such as using 1 hour:

```php
add_filter( 'ptc_completionist_request_tokens_ttl', 'ptc_get_request_tokens_ttl', 10, 1 );
function ptc_get_request_tokens_ttl( $ttl ) {
  return HOUR_IN_SECONDS;
}
```

Refer to [WordPress's PHP time constants](https://codex.wordpress.org/Easier_Expression_of_Time_Constants) for other duration expressions.

### Clearing the cache

Cache entries relate to each WordPress post that contains Completionist shortcodes and are stored on an individual basis as postmeta. For this reason, cache entries are purged for a post whenever it is updated. To ensure your Asana updates are immediately reflected on WordPress, you can simply click "Update" in the WordPress post editor to clear the Asana cache for that post.

To purge all Asana cache entries across all posts, simply click *Save* next to [the *Frontend Authentication User* option](/completionist/getting-started/#set-a-frontend-authentication-user) in Completionist's Settings screen.

## Untitled Project Sections

Despite an Asana project seeming to have untitled sections or no sections at all, the Asana API provides these sections with placeholder names. To display the same experience, Completionist ignores those placeholder names.

**By default, Completionist does not display these section titles:**

- `(no section)`
- `untitled section`
- `Untitled section`
- `Untitled Section`

You may choose to override which project section names are ignored by filtering the list of erased names. The Asana project's GID and request configuration arguments are also provided for context.

This will allow all section names to be displayed, including Asana's placeholder names:

```php
add_filter( 'ptc_completionist_project_section_names_to_erase', 'ptc_get_project_section_names_to_erase', 10, 3 );
function ptc_get_project_section_names_to_erase( $names, $project_gid, $args ) {
  return array();
}
```

This will add another section name to be erased:

```php
add_filter( 'ptc_completionist_project_section_names_to_erase', 'ptc_get_project_section_names_to_erase', 10, 3 );
function ptc_get_project_section_names_to_erase( $names, $project_gid, $args ) {
  $names[] = 'Section Name';
  return $names;
}
```

## [ptc_asana_project]

Displays Asana project information and tasks.

<div class="banner banner-info">
  <p>Only "list" layout is displayed in the free version of Completionist. Additional layouts such as "calendar" are available to Completionist Pro users only.</p>
</div>

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

**Quick Copy (with default values):**

```
[ptc_asana_project src="<ASANA_PROJECT_URL>" auth_user="" exclude_sections="" show_name="true" show_description="true" show_status="true" show_modified="true" show_due="true" show_tasks_description="true" show_tasks_assignee="true" show_tasks_subtasks="true" show_tasks_completed="true" show_tasks_due="true" show_tasks_attachments="true" show_tasks_tags="true"]
```

<div class="banner banner-warning">
  <p><strong>Remember</strong> to change the <code>src</code> attribute value to the URL of the Asana project that you'd like to display!</p>
</div>
