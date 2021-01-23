---
title: Getting Started
parent: Completionist
nav_order: 1
---

# Getting Started
{: .no_toc }

Simply connect your Asana account and choose a tag to start managing Asana tasks on your WordPress site.
{: .text-beta .fw-300 .text-grey-dk-000}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Install the Plugin

Completionist may be installed by extracting the zip file contents into your `wp-content/plugins/` directory or by using the built-in WordPress plugin installer:

1. Download the Completionist WordPress plugin for free from [the Purple Turtle Creative website](https://purpleturtlecreative.com/completionist/).
2. Log into your WordPress admin area and navigate to *Plugins > Add New*.
3. Click *Upload Plugin* at the top of the screen.
4. Upload the Completionist zip file and click *Install Now*.
5. Activate the plugin once the plugin is installed successfully.

<div class="banner">
  <h3>
    WordPress Multisite (wpmu) Considerations
  </h3>
  <p>
    Completionist is fully compatible with WordPress multisite networks. Feel free to activate the plugin at the network level or per blog/subsite. If you decide to uninstall Completionist, all plugin data will be properly removed across your network.
  </p>
</div>

## Connect Your Asana Account

<div class="banner banner-danger">
  <h3>
    Asana Account Required
  </h3>
  <p>
    Completionist depends on an Asana account connection to function. <a href="https://asana.com/create-account" target="_blank">Create an Asana account</a> for free before continuing this setup guide.
  </p>
</div>

1. Navigate to the Completionist settings screen by clicking *Completionist* toward the bottom of your WordPress admin menu.
2. In a new browser window, sign into your Asana account and [visit your Asana developer console](https://app.asana.com/0/developer-console).
3. Click to generate a new access token at the bottom of your Asana developer console and follow the prompts.
4. Back in Completionist, paste your Personal Access Token into the Asana Connect form, agree to let Completionist perform actions in your Asana account on your behalf, and click *Authorize*.
5. Once successfully connected, you'll now be able to access Completionist's settings.

## Set a Site Tag

The final step to get started using Completionist is to set a *"site tag"*. A site tag is required to use Completionist to avoid hitting API limits and to ensure only relevant tasks are displayed.

1. In the Completionist settings screen, find the workspace settings section.
2. Choose an Asana workspace. After making your selection, the tag options will be retrieved for selection.
3. Once the tag options for your chosen workspace have loaded, choose the tag that Completionist will use to associate Asana tasks to your WordPress site.
4. Click *Save* to confirm your chosen workspace and site tag.

<div class="banner">
  <h3>
    Site Tag Basics
  </h3>
  <p>
    To ensure task lists in your WordPress area remain relevant and tidy, Completionist only retrieves Asana tasks with the chosen tag.
  </p>
  <p>
    When you no longer want Completionist to display the task on your WordPress site, simply remove the site tag from the task in Asana. If you instead remove the task from within your WordPress site using Completionist, the site tag will be removed from the task in Asana for you.
  </p>
</div>

