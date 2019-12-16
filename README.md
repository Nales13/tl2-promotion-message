# Plugin: `tl2-promotion-message`

Adds a system message that is sent whenever a user is promoted to trust level 2.

---

## Features

- Sends a system message whenever a user is promoted to trust level 2, similarly to the system message that happens when a user gains trust level 1.

  - Discourse does not provide this feature out of the box.

  - The message can be customized via the text customization tab in the admin panel of the forum, and can also be translated into different locales there.

---

## Impact

### Community

Trust level 1 users that are ranked up (manually or automatically) to trust level 2 now get a clearer notification of this event and are linked to additional resources they should review about appropriate forum behavior, considering they now have additional forum permissions.

### Internal

Fewer inquiries from the community to Developer Relations about trust level 2.

### Resources

A highly negligible workload whenever someone is promoted to trust level 2, which is an infrequent event.

### Maintenance

The welcome message needs to be kept up-to-date by Developer Relations. Developer Relations should also translate the message into whatever languages we currently support on the Developer Forum, either by committing it to this repository as locale files, or by setting it through text customization in the admin panel on the forum.

---

## Technical Scope

The plugin hooks into the method that is called whenever a user's trust level is changed.

The prepend mechanism that is used to intervene in this method is a standard one, and so is unlikely to break throughout Discourse updates, with the exception of the case where the name or parameter list of `Promotion.change_trust_level!` changes. Even if that happens, the forum will continue to function properly, only the plugin functionality will be broken.

<!---
TODO: uncomment this when plugin adjusted

The plugin uses the integrated `DiscourseEvent.on(:user_added_to_group)` to find out whenever a user is added to the trust_level_2 group, which means they have just become trust level 2 users.

Since DiscourseEvent provides a highly explicit contract about the event, it is unlikely for the plugin functionality to break throughout Discourse updates. The event would have to be deprecated and no longer triggered in Discourse source for the plugin to stop working. In the unlikely case that happens, nothing apart from the plugin itself should break at that point, the forum will continue to function.
-->

---

## Configuration

After installation, the text of the promotion message can (and should) be modified via the following locale entries:

- Subject: `system_messages.welcome_tl2_user.subject_template`

- Body: `system_messages.welcome_tl2_user.text_body_template`

Locale entries can be modified at `%BASEURL%/admin/customize/site_texts`.

The default text provided by this plugin is not suitable to be used as actual promotion message and must be edited to include the right content at that point in time.
