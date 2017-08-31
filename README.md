# Slack chat plugin for Redmine

This plugin posts updates to issues in your Redmine installation to a Slack
channel. It varies from the source repository in that it will only post to Slack
if the specified string token is present in the journal notes. 

## Push token

If you are worried about too much cross-posting, and would only like certain *important*
messages to make their way into Slack, we have the solution! Under the original version
of this integration, our manager accounts (set to receive emails about all Redmine events)
started to become inundated with two emails and a Slack notification for every Redmine
update, and our project channels quickly became polluted with way too many Redmine updates
to have a useful discussion history. So we decided to remove the Slack integration.
However, our developers (set to only receive emails on issues they are assigned to or
watching) started to miss notifications, and lost real-time notifications for our group
and needed a way to indicate when we wanted to push a notification to Slack of a Redmine
event. Thus, the push token was born!

The push token makes it explicit which messages will be sent to your Slack project channels.
Unless you inclue the `#slack` tag within your message, no integration will happen. Simple
as that!

**Example message that will NOT be pushed to Slack project channel**

```
I did a minor cleanup today to fix some documentation and spelling mistakes. Still a 
lot of work to go on this Feature!
```

**Example message that WILL be pushed to Slack project channel**

```
Hey, @johndoe can you comment on the decision to use non-overlapping hashes in this
code instead of overlapping hashes? I think we have hurt our accuracy with this
choice.

#slack
```

The token can appear anywhere in the message, not just at the end. You can use "@" 
references to call out people on your Team too.

## Screenshot

![screenshot](https://raw.github.com/sciyoshi/redmine-slack/gh-pages/screenshot.png)

## Installation

From your Redmine plugins directory, clone this repository as `redmine_slack` (note
the underscore!):

    git clone https://github.com/sciyoshi/redmine-slack.git redmine_slack

You will also need the `httpclient` dependency, which can be installed by running

    bundle install

from the plugin directory.

Restart Redmine, and you should see the plugin show up in the Plugins page.
Under the configuration options, set the Slack API URL to the URL for an
Incoming WebHook integration in your Slack account.

## Customized Routing

You can also route messages to different channels on a per-project basis. To
do this, create a project custom field (Administration > Custom fields > Project)
named `Slack Channel`. If no custom channel is defined for a project, the parent
project will be checked (or the default will be used). To prevent all notifications
from being sent for a project, set the custom channel to `-`.

For more information, see http://www.redmine.org/projects/redmine/wiki/Plugins.
