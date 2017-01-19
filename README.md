# Goal #
Work in an Agile way and build a Continuous Integration / Continuous Deployment (CI/CD) pipeline to build, test, and deploy a containerized stateful web application:

![Diagram of Goal](https://git.corp.netapp.com/madden/hackathon-vol2/uploads/07c5312a6b80dacf063bcea6954a488e/hack-vol2.png)

To start out everyone will get on Slack and Trello so we can work using a ChatOps model popular in DevOps shops.  Slack is a communications platform (chat on steroids) and Trello helps with task management which will help you keep your actions and status in check.  You will do most work on your own container host running CoreOS, an OS optimized for containers which includes Docker pre-installed.  From that host you will install and configure the NetApp Docker Volume Plugin and provision some NetApp SolidFire storage.  Then you will deploy a web application and database and test it works properly.  Next you will setup Jenkins, including integration with Slack, so that you can quickly test and deploy new releases of the app that will be rolled out during the event.  **Lets get to it!**

Technologies used:

- Docker as the container engine
- Jenkins as the CI/CD engine
- SolidFire with the NetApp Docker Volume Plugin for persistent storage
- Web application written in Node.js and Javascript
- Redis in-memory data structure store as database

# Summary of Stages #

1. Get ready for ChatOps:  Join Slack and Trello
1. Setup nDVP
1. Install Web Application Manually
1. Initial setup Jenkins
1. Build a job that will perform automated testing of new commits

### [1] Get ready for ChatOps:  Join Slack and Trello ###
1. [Slack](https://www.slack.com) is software used for communicating within teams.  In this event we will use it for Q/A as well as updates from other tooling. Please create an account and sign in at [NetApp Hackathon](https://netapp-hackathon.slack.com/).  If you use your @netapp.com email address you will automatically be approved for access.  Once you have joined post a welcome message announcing yourself on the #general channel!  There are a few other channels that the bots will post to:
 - #workflow: Trello sourced task completion updates
 - #build: Jenkins sourced job updates
 - #git: Git sourced source code and issue updates
1. Send the leader a private message on Slack asking for credentials for this event.  Please only ask once for each team as a container host will be allocated to your team in the response.  Only if you will not use Trello can you click [here](TRELLO.md) to find instructions for the event, otherwise use those in Trello.

## Acknowledgements ##

Special thanks to [Andrew Sullivan](https://github.com/acsulli) for Jenkinsfile snippets and inspiration, [Kai Davenport](https://github.com/binocarlos) for the basis of the stateful app, and Jason Padman and Kapil Arora for their dry-run to validate the steps!

## CLI hints ##

If you don't use Linux and Docker everyday here are some useful commands:

| Command     | Description     |
| :------------- | :------------- |
| `sudo -i`     | Superuser do interactively.  Basically change your shell to the root user so you don't need to type sudo anymore.   |
| `ls -ltr`     | Show all files in a directory, reverse sorted by modification timestamp.  Useful to find the most recently modified file.|
| `history`     | Show previous commands entered|
| `docker --help` | Show help for docker.  Available at each level, so `docker volume --help` will give help syntax for volumes |
| `/var/log/netappdvp/error.log` | Error log for the nDVP.  If something isn't working check here |