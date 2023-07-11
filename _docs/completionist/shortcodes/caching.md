---
title: Caching
parent: Shortcodes
grand_parent: Completionist
nav_order: 1
---

# Shortcode Caching
{: .no_toc }

Understand and customize how Asana data is cached and used within WordPress.
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

## Changing the cache TTL

**Frontend requests are cached by default for 15 minutes.** This immensely improves website performance by reducing how often data is requested from Asana.

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

## Clearing the cache

Frontend caching and security is managed by the `Request_Token` PHP class within Completionist. You can think of request tokens as WordPress nonces. All related data is stored within the `wp_ptc_completionist_request_tokens` database table.

Request tokens are created in PHP as they are needed, including their associated cache records. Feel free to truncate the table at any time, but note that any frontend HTML caching of your WordPress website might become out-of-sync. For this reason, you should also clear the PHP/HTML cache for each page that contains a Completionist shortcode.

You can clear the request tokens database table by using PHP:

```php
// Require the Request_Token class file.
require_once PTC_Completionist\PLUGIN_PATH . 'src/public/class-request-token.php';
// Delete all request token data, including cache records.
PTC_Completionist\Request_Token::delete_all();
// @TODO - Clear HTML cache records.
```
