# Welcome!

This quick intro document should help you get up to speed on the
following topics:

- Where do I find shared libraries?
- Is there any documentation?
- How do I set up DHIS2 for local development?
- Where do we track issues?
- What is our Way of Work?
- How do I deploy... apps? libs? dhis2?
- Where do I get help from an actual human being?

# Where is the team at?

We use Slack to collaborate and talk to each other when at the keyboard. Feel free to talk to people AFK too. Some channels you should join are: **#frontend**, **#general**, **#announcements**, **#webapi**, **#devops**.

Use your @dhis.org e-mail to sign up.

- [Slack](https://dhis2.slack.com/)

# Documentation

Every app has its own README which should include most info you need. There is also a wealth of information in
the online documentation:

- [DHIS2 Frontend docs](https://dhis2.github.io/)
- [DHIS2 Web API docs](https://docs.dhis2.org/master/en/developer/html/webapi.html)
- [DHIS2 User/Implementer/Developer/End user Documentation](https://www.dhis2.org/documentation)
- [DHIS2 Development docs](https://www.dhis2.org/development)

## Automatic build systems

- [Travis](https://travis-ci.org/)
- [Jenkins](https://ci.dhis2.org/)

## Mailing lists

There are two mailing lists which we use to interact with the DHIS2
community world-wide.

- [dhis2-users@lists.launchpad.net](https://lists.launchpad.net/dhis2-users/)
- [dhis2-devs@lists.launchpad.net](https://lists.launchpad.net/dhis2-devs/)

## Issue tracking

### Functional

- [JIRA](http://jira.dhis2.org/)

### Technical

- Every app has its own issue tracker on Github where technical issues
  are documented.

# Development

## Setup DHIS2

You will need an instance of DHIS2 running so your webapps have an API
to talk to. You can run this in
[Docker](https://github.com/dhis2/dhis2-docker), VirtualBox, Vagrant, or
just as a plain-old-java with tomcat or jetty combo.

- [DHIS2 Setup instructions](dhis2-basic-setup.md)

## Whitelist your local frontend apps in DHIS2 settings

If you want to locally work on front-end apps, make sure to add `http://localhost:8081` (*without a trailing slash!*)
to your CORS whitelist in the [DHIS2 settings app](http://localhost:8080/dhis/dhis-web-settings/#/access) via:

`> apps> system_settings> access> cors_whitelist`

## Shared libraries

We have a set of shared libraries which should be used in webapps to
standardise the way we interact with the DHIS2 instances.

- [d2](https://github.com/dhis2/d2)
- [d2-ui](https://github.com/dhis2/d2-ui)

## Code and repository convention

- [Repository guidelines](GUIDELINES.md)
- [eslint-config-dhis2](https://github.com/dhis2/eslint-config-dhis2)
- [editorconfig](https://www.editorconfig.org) (per project)
- [JSDoc](https://github.com/jsdoc3/jsdoc)
    Minimum is a function description:
    ```
    /** This is a description for foo */
    function foo() {}
    ```
    Note that jsdoc **only** scans comments that starts with two stars: `/**`

## A new frontend app

- Use [create-react-app](https://github.com/dhis2/eslint-config-dhis2)
  as a starting point

# Way of Work

## Cheatsheet

1. clone your repo
2. checkout a new branch for the work you are going to do
3. do some changes
4. commit
5. repeat 3-4
6. open a pull request
7. ask someone on slack #frontend if they can have a look
8. merge PR
8. a. some apps require that you deploy now
8. b. for other apps you are done now

## Versioning

The basic principle is to follow semver (major.minor.patch).

- Major is used to track against the DHIS2 version (e.g. 28 for DHIS2 version 2.28)
- Minor for marking breaking changes
- Patch is for fixes and patches

**N.B. Check the README for the instructions for your specific app**

## Deployment

There are multiple meanings to "deploy" within the DHIS2 ecosystem.

### to NPM

On one hand, when talking about d2 and d2-ui a deployment means creating
a tag based on the commit which bumps the version in `package.json`, and
pushing the resulting tag to the Github repo.

```
$ yarn version
% <major.minor.patch>
$ git push
$ git push --tags
```

When a tag is pushed to the repo, Travis will run a build and then
publish the artifact to NPM.

### to DHIS2

On the other hand, most apps we build need to be deployed to a DHIS2
instance.

Core applications, like the maintenance-app, are bundled with the DHIS2
WAR-file in each release and shipped as the "core" application suite.

This way of shipping core-apps is being phased out, but as of 2.29 it is
still the primary way of shipping core applications.

Refer to the documentation for the API on how to work with [apps inside of a DHIS2 context](https://docs.dhis2.org/master/en/developer/html/webapi_apps.html).

