---
title: Automated Tasks
parent: Completionist
nav_order: 4
---

# Automated Tasks
{: .no_toc }

Create Asana tasks automatically as events occur on your WordPress site to standardize task workflows.
{: .text-beta .fw-300 .text-grey-dk-000}

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## List All Automations

Completionist allows you to automatically create tasks in Asana as WordPress events occur on your website.

To access the Automations screen, navigate to Completionist > Automations in your WordPress admin.

## Create an Automation

Add a new automation to create Asana tasks as WordPress events occur on your website.

1. In the Completionist > Automations screen, click the button in the top-right corner labeled "Add New".
2. Input a *Title* and *Description* for your new Automation. These details will be displayed in the Automations listing and help with internal documentation.
3. Select the *Trigger Event* for the Automation. This determines which WordPress event (action hook) will execute the automation. There are currently two groups of options, each corresponding to WordPress action hooks:
   - User Events
      - User is Created – `user_register`
      - User is Updated – `profile_update`
      - User is Deleted – `delete_user`
   - Post Events
      - Post is Created – `wp_insert_post`
      - Post is Updated – `post_updated`
      - Post is Trashed – `trash_post` Note that this is when a post is moved to the trash rather than being permanently deleted from the trash.
4. If needed, click the *Add Condition* button to limit the Automation to only execute when certain conditions are met. There are several properties and comparison operators to choose. The property options for the Conditions will change depending on the category of the selected *Trigger Event* (User or Post). All conditions must be met (true) for the Automation to execute—which is to say the Conditions are assessed using logical AND.
5. Finally, click the *Add Action* button to define the Actions for the Automation. When the Trigger Event fires and all Conditions have been met, then all Actions will execute. Currently, the only supported Action option is *Create Asana Task* which features the following inputs:
   - Task name – The title of the Asana task.
   - Creator – The Asana user designated as the task creator. Only users that have connected their Asana account to the Completionist plugin are able to be selected.
   - Assignee – The Asana user designated as the assignee. Only users that have connected their Asana account to the Completionist plugin are able to be selected.
   - Due Date – A static due date for the Asana task.
   - Project – The Asana project to which the task will be added.
   - Description – The description text of the Asana task.
   - Pin to Post – A WordPress post to which the new Asana task will be pinned. Type in the field to search for a WordPress post by name, and then select it in the list.
6. Click the large *Create* button at the bottom of the page to add the new Automation.

## Review Automation Statistics

In the main Automations screen, all Automations are listed with useful information:

- Automation Details
  - Title
  - Last Modified
  - Description
- Conditions – The number of Conditions for the Automation.
- Actions – The number of Actions for the Automation.
- Triggers – The number of times the Actions have executed.
- Last Triggered – The time of the most recent execution of the Actions.

## Edit an Existing Automation

There are three ways to update an Automation in Completionist. You may (1) click the Automation's title in the main listing, (2) hover the Automation row in the main listing and click the revealed *Edit* button, or (3) access the edit screen directly by URL.

To find an Automation's ID, hover the Automation's title in the main listing. In the edit screen for the Automation, the ID is referenced in the `automation` query param like so:

```
/wp-admin/admin.php?page=ptc-completionist-automations&automation=2
```

## Delete an Existing Automation

In the main Automations listing, hover the Automation row and click the revealed *Delete* button.

If you'd instead like to keep the Automation but temporarily prevent it from executing, see [*Disable an Existing Automation*](#disable-an-existing-automation).

## Disable an Existing Automation

There is no official user interface for temporarily disabling an Automation; however, you can add a Condition to the Automation that you know will always be false. If you do this, it's also a good idea to note this on the Automation so that it is visible in the main listing, such as adding `[DISABLED]` somewhere in the title or description.

