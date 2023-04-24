---
title: Customizations
parent: Shortcodes
grand_parent: Completionist
nav_order: 1
---

# Shortcode Customizations
{: .no_toc }

Use PHP and JavaScript hooks to customize shortcode content, functionality, and styles to suite your needs.
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


## Enqueueing Custom Assets

In the `'wp_footer'` action hook of WordPress, Completionist enqueues the scripts and styles for each of its shortcodes that have rendered for the current page load. As Completionist processes each detected shortcode tag, the `'ptc_completionist_shortcode_enqueue_assets'` action hook in PHP is executed for third-party customizations.

Note that this action hook only runs for shortcodes that have been executed. This ensures assets are enqueued only once per page load and only when they are needed.

This sample code enqueues a custom JavaScript file and CSS stylesheet whenever [the `[ptc_asana_project]` shortcode](/completionist/shortcodes/#ptc_asana_project) has been rendered at least once for the current page load:

```php
add_action(
  'ptc_completionist_shortcode_enqueue_assets',
  'custom_completionist_shortcode_enqueue_assets',
  10,
  1
);

function custom_completionist_shortcode_enqueue_assets( string $shortcode_tag ) {
  if ( 'ptc_asana_project' === $shortcode_tag ) {
    
    wp_enqueue_script(
      'custom-asana-project-script',
      plugins_url( '/assets/js/script.js' , __FILE__ ),
      array( 'ptc-completionist-shortcode-asana-project' ),
      '1.0.0',
      true
    );
    
    wp_enqueue_style(
      'custom-asana-project-styles',
      plugins_url( '/assets/css/styles.css' , __FILE__ ),
      array( 'ptc-completionist-shortcode-asana-project' ),
      '1.0.0'
    );
  }
}
```

*See WordPress's documentation for usage of [`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) and [`wp_enqueue_style()`](https://developer.wordpress.org/reference/functions/wp_enqueue_style/).*

## JavaScript Hooks

Completionist uses [WordPress's `@wordpress/hooks` npm package](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-hooks/) to implement custom action and filter hooks in JavaScript.

Using [the method described above](#enqueueing-custom-assets), enqueue a custom JavaScript file that registers your modifications.

This example customizes the project section "Section" label text in Completionist Pro:

```js
window.Completionist.hooks.addFilter(
  'task_modal_project_section_label',
  'my-custom-plugin',
  ( label, task ) => {

    // Project section names acting as statuses.
    const statuses = [
      'To Do',
      'In Progress',
      'Needs Review',
      'Done',
    ];
    
    if ( statuses.includes( task.project_section_name ) ) {
      // Label the project section as a "Status".
      label = 'Status';
    }

    return label;
  }
);
```

