# Rundeck Slack bot

Trigger your [Rundeck](http://rundeck.org) jobs from [Slack](https://slack.com).

_Example:_

    @rundeckbot deploy user-service 1.0 to staging
    
    > rundeckbot:
    > OK, I'm deploying user-service version 1.0 to staging.
    > Status of job is: running
    > Details: http://rundeck/jobs/abc/123
    
> Why would you want this? Check out [ChatOps](http://blogs.atlassian.com/2016/01/what-is-chatops-adoption-guide/).

## What can it do?

##### Trigger your deployment jobs

<img alt="Deploy" src="https://github.com/outofcoffee/rundeck-slackbot/raw/master/docs/images/deploy.png" width="467">

##### Trigger your other custom jobs

<img alt="Restart" src="https://github.com/outofcoffee/rundeck-slackbot/raw/master/docs/images/restart.png" width="472">

##### Lock things to prevent accidental deployment

<img alt="Lock deployment failure" src="https://github.com/outofcoffee/rundeck-slackbot/raw/master/docs/images/lock_deploy_fail.png" width="371">

##### Unlock things you've locked

<img alt="Unlock job" src="https://github.com/outofcoffee/rundeck-slackbot/raw/master/docs/images/unlock.png" width="336">

##### Get help

<img alt="Help" src="https://github.com/outofcoffee/rundeck-slackbot/raw/master/docs/images/unknown.png" width="389">

## Instructions

* As a Slack admin, create a Slack bot user and obtain its auth token 
* As a Rundeck admin, generate a Rundeck API token
* Set environment variables
* Run!

## Quick start

The quickest way to get up and running is to use the Docker image:

    docker run -d \
            --env SLACK_AUTH_TOKEN="CHANGEME" \
            --env SLACK_CHANNEL_NAME="rundeck-slackbot" \
            --env RUNDECK_API_TOKEN="CHANGEME" \
            --env RUNDECK_BASE_URL="http://rundeck:4440" \
            -v /path/to/actions.yml:/opt/rundeck-slackbot/actions.yml \
            outofcoffee/rundeck-slackbot

Note: the container doesn't require any inbound ports to be exposed.

## Build

If instead you wish to build and run locally, you can run:

    ./gradlew installDist
    docker-compose build

Once built, set the following environment variables in `docker-compose.yml`:
    
    SLACK_AUTH_TOKEN: "CHANGEME"
    SLACK_CHANNEL_NAME: "rundeck-slackbot"
    RUNDECK_API_TOKEN: "CHANGEME"
    RUNDECK_BASE_URL: "http://rundeck:4440"
    BOT_CONFIG: "/path/to/actions.yaml"
    
> Note: the default path for _BOT_CONFIG_ is `/opt/rundeck-slackbot/actions.yml`

Then run with:

    docker-compose up

If you change anything, don't forget to rebuild before running again.

## More info

Slack API: https://api.slack.com/bot-users

Rundeck API: http://rundeck.org/2.6.9/api/index.html#running-a-job

### Rundeck

Any Rundeck instance can be used as long as it supports API v14 or higher.

As an example, here is an unofficial Rundeck Docker image: https://hub.docker.com/r/jordan/rundeck/

    docker run -it \
        -p 4440:4440 \
        -e SERVER_URL=http://localhost:4440 \
        jordan/rundeck

## Roadmap

* Notify lock owner on unlock
* Last deployment query (what version, who triggered it etc.)

## Contributing

Pull requests are welcome.

## Author

Pete Cornish (outofcoffee@gmail.com)
