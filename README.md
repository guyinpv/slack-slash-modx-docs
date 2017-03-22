# MODX Docs Slash Command for Slack
This code was written to provide a simple way to search the MODX docs from within Slack.

A user can simply type `/docs` and they will get some helpful top-level links at the MODX docs website.

If they type `/docs my search terms`, this script will search the MODX docs and parse the results into a set of links and return them to Slack. If nothing is found, the script will return this as well as a link to the search query in case you want to try the search manually.

## How to Create the Slash Command

Log in to Slack and go to the [Slack app management page](https://slack.com/apps/manage).

Click "Custom Integrations" on the left sidebar. If you see "Slash Commands", click it. Then click the "Add Configuration" green button.
If you don't see the Slash Commands link, just click "Build" in the main menu at the top of the page on the right. Then click "Start Building". Then finally click "Create an App".

In the popup, give the app a name, choose a team, and click "Create App".

Choose "Slash Commands" from the features area.

Click to create a new command.

On the Create New Command screen, fill in the details. The "Request URL" should point to the PHP endpoint, this script, wherever you will be hosting it, such as "example.com/slack-slash-modx-docs.php".
You don't need to turn on escaping users and links.

Finally click the "Save" button.

## How to Use This Script

This is just a small, uncomplicated PHP script contained in a single file with no dependencies except for having cURL available.

Upload the script to your server anywhere it can be accessed, such as "example.com/slack/slack-slash-modx-docs.php". This URL must be the same as what is set up in Slack.

Edit the PHP file and change the `$token` and `$command` variables to match what you set up at Slack. The script already has "/docs" but if you created a different command, put that in there instead, and keep the leading forward slash.

## Test

If the PHP script and the slash command both have the same token, command, and URL, it would be available and work immediately in the Slack app. Type `/docs` and you should see the Slack suggestions pop up with the command in there already. Click <enter> a couple times and you should get a list of helpful links.

Type it again with a search term such as `/docs snippet` and it should give the same search results as the MODX docs website.

## Troubleshoot

The script carefully checks that the token and command match or else it returns an HTTP 403 "Forbidden" header. This prevents people from simply opening the URL to run the script. It also prevents other Slack networks from using the endpoint since they won't have the same token.

Double-check the token matches and the `$command` variable has the correct slash command with a leading forward slash, such as "/docs".

If it still returns nothing, it is likely a PHP error or the script is dying somehow from a different problem. You can use a REST client to test POSTing to the URL, such as Postman in Google Chrome. Sometimes if there is a PHP error, depending on where it happens in the script, the error text might even output into Slack!  
