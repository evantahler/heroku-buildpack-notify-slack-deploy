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
1. Add this buildpack: `heroku buildpacks:set https://github.com/evantahler/heroku-buildpack-notify-slack-deploy.git` (or add it via the heroku dashboard if you have multiple buildpacks)

## Optional - Github Commit Information

By default, there's very little information about the commit that we can get from Heroku. However, we can curl the Github API and try to learn more about the commit. If you set the following additional environment variables, we can load the commit information, committer, and URL from Github:

- `DEPLOY_NOTIFY_GITHUB_AUTH_TOKEN`: A Github PAT Token. You can generate one [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- `DEPLOY_NOTIFY_GITHUB_ORG`: The name of your Github Org (or Github User Name)
- `DEPLOY_NOTIFY_GITHUB_PROJECT`: The name of your Github Project

Now, the message in Slack can look like:

```
*my-heroku-app* was deployed - Deploy 04a2729b
> Evan Tahler - evan.tahler@company.com
> Fix all the bugs and make everything great
https://github.com/COMPANY/PROJECT/commit/abc123
```
