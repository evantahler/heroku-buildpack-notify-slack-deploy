# heroku-buildpack-notify-slack-deploy

This is a Heroku Buildpack you can add to your heroku deployments that will notify a slack channel every time your application is deployed.

## Configuring your Slack Applicaiton
1. Visit https://api.slack.com/incoming-webhooks to create a new Slack Application which can recieve a webook. You only need the "Incomming Webhooks" feature.
2. As part of the configuration, you will choose a workspace and channel to connect the application to.
3. take note of the webook URL, which looks something like this `https://hooks.slack.com/services/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S`
4. Feel free to configure the app's icon and name!

## Adding to Heroku
1. Enable Dyno Metadata for yoru application `heroku labs:enable runtime-dyno-metadata`
1. Save your new webook URL as a Herou config setting for the varaible`SLACK_DEPLOYMENT_WEBHOOK_URL`, ie: `heroku config:set SLACK_DEPLOYMENT_WEBHOOK_URL="https://hooks.slack.com/services/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S"`
2. Add this buildpack: `heroku buildpacks:set https://github.com/evantahler/heroku-buildpack-notify-slack-deploy.git` (or add it via the heroku dashboard if you have multiple buildpacks)
