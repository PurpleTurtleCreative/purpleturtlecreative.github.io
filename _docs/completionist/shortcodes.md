---
title: Shortcodes
parent: Completionist
nav_order: 5
has_children: true
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

Frontend caching and security is managed by the `Request_Token` PHP class within Completionist. You can think of request tokens as WordPress nonces. All related data is stored within the `wp_ptc_completionist_request_tokens` database table.

Request tokens are created in PHP as they are needed, including their associated cache records. Feel free to truncate the table at any time, but note that any frontend HTML caching of your WordPress website might become out-of-sync. For this reason, you should also clear the PHP/HTML cache for each page that contains a Completionist shortcode.

You can clear the request tokens database table by using PHP:

```php
// Require the Request_Token class file.
require_once \PTC_Completionist\PLUGIN_PATH . 'src/public/class-request-token.php';
// Delete all request token data, including cache records.
\PTC_Completionist\Request_Token::delete_all();
// @TODO - Clear HTML cache records.
```



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

**Quick Copy (with default values):**

```
[ptc_asana_project src="<ASANA_PROJECT_URL>" auth_user="" exclude_sections="" show_name="true" show_description="true" show_status="true" show_modified="true" show_due="true" show_tasks_description="true" show_tasks_assignee="true" show_tasks_subtasks="true" show_tasks_completed="true" show_tasks_due="true" show_tasks_attachments="true" show_tasks_tags="true"]
```

_**\*\*Remember** to change the `src` attribute value to the URL of the Asana project that you'd like to display!_


## [ptc_asana_project_list]

Displays a WordPress user's associated Asana projects' information and tasks.

<div class="banner banner-warning">
  <p>⭐️ This shortcode is available to Completionist Pro users only.</p>
</div>

**Attributes:**

This shortcode shares the same attributes as the singular `[ptc_asana_project]` shortcode plus the following:

- `layout` – Optional. The Asana project layout for all listed projects. Default 'list'.
  - Possible values are `list` and `calendar`
- `user` – Optional. A WordPress user's ID to determine which Asana projects to list. Defaults to the currently logged-in user.
  - See the "Asana Projects" setting in the WordPress user's profile to select which Asana projects the WordPress user is allowed to view.

**Quick Copy (with default values):**

```
[ptc_asana_project_list layout="list" user="" auth_user="" exclude_sections="" show_name="true" show_description="true" show_status="true" show_modified="true" show_due="true" show_tasks_description="true" show_tasks_assignee="true" show_tasks_subtasks="true" show_tasks_completed="true" show_tasks_due="true" show_tasks_attachments="true" show_tasks_tags="true"]
```
