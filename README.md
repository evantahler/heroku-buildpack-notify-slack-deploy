# heroku-buildpack-notify-slack-deploy

This is a Heroku Buildpack you can add to your Heroku deployments that will notify a Slack channel every time your application is deployed.

![screenshot](https://raw.githubusercontent.com/evantahler/heroku-buildpack-notify-slack-deploy/master/sceenshot.png)

## Configuring your Slack Applicaiton

1. Visit https://api.slack.com/incoming-webhooks to create a new Slack Application that can receive a webook. You only need the "Incomming Webhooks" feature.
2. As part of the configuration, you will choose a workspace and channel to connect the application to.
3. Take note of the webook URL, which looks something like this `https://hooks.slack.com/services/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S`
4. Feel free to configure the app's icon and name!

## Adding to Heroku

1. Enable Dyno Metadata for your application `heroku labs:enable runtime-dyno-metadata`
1. Save your new webook URL as a Heroku config setting for the variable`SLACK_DEPLOYMENT_WEBHOOK_URL`, i.e.: `heroku config:set SLACK_DEPLOYMENT_WEBHOOK_URL="https://hooks.slack.com/services/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S"`
1. Add this buildpack via the Heroku dashboard (the `heroku buildpack:set` command will replace any buildpacks you already have).  
  * **Note:** Be sure that this buildpack is the final buildpack in your app - the order matters!

![buildpack](https://raw.githubusercontent.com/evantahler/heroku-buildpack-notify-slack-deploy/master/buildpack.png)

## Optional - Github Commit Information

By default, there's very little information about the commit that we can get from Heroku. However, we can curl the Github API and try to learn more about the commit. If you set the following additional environment variables, we can load the commit information, committer, and URL from Github:

- `DEPLOY_NOTIFY_GITHUB_AUTH_TOKEN`: A Github PAT Token. You can generate one [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
Important note: you *must* grant _repo_ access when creating this PAT Token, or else it will default to "Public Access" and won't work!
- `DEPLOY_NOTIFY_GITHUB_ORG`: The name of your Github Org (or Github User Name)
- `DEPLOY_NOTIFY_GITHUB_PROJECT`: The name of your Github Project (i.e. repository name)

Now, the message in Slack can look like:

```
*my-heroku-app* was deployed - Deploy 04a2729b
> Evan Tahler - evan.tahler@company.com
> Fix all the bugs and make everything great
https://github.com/COMPANY/PROJECT/commit/abc123
```
