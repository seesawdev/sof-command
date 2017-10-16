# @atomist/sof-command

[![Build Status](https://travis-ci.org/atomist/automation-seed-ts.svg?branch=master)](https://travis-ci.org/atomist/automation-seed-ts)

This repository contains examples demonstrating use of
the [Atomist][atomist] API.  You will find examples illustrating:

-   Creating bot commands using _command handlers_

These example use the [`@atomist/automation-client`][client] node
module to implement a local client that connects to the Atomist API.

[client]: https://github.com/atomist/automation-client-ts (@atomist/automation-client Node Module)

## Prerequisites

### Enroll the Atomist bot in your Slack team

TODO

### Node.js

You will need to have [Node.js][node] installed.  To verify that the
right versions are installed, please run:

```
$ node -v
v8.4.0
$ npm -v
5.4.1
```

[node]: https://nodejs.org/ (Node.js)

### Cloning the repository and installing dependencies

To get started run the following commands:

```
$ git clone git@github.com:atomist-blog/sof-command.git
$ cd sof-command
$ npm install
```

### Configuring your environment

For the client to connect and authenticate to the Atomist API,
a [GitHub personal access token][token] with `read:org` scope is
required.  Once you have obtained the GitHub personal access token,
make it available to the client by exporting it into an environment
variable:

```
$ export GITHUB_TOKEN=<your token goes here>
```

Alternatively you can also place the token in `src/atomist.config.ts`.
Replace

```typescript
const token = process.env.GITHUB_TOKEN;
```

with

```typescript
const token = "your token goes here";
```

*If you  add the token  to the `atomist.config.ts`, please  do **not**
commit the file and push it to GitHub.com.*

[token]: https://github.com/settings/tokens (GitHub Personal Access Tokens)

The Atomist API will only allows members of the GitHub team
`atomist-automation` to authenticate and register a new client.  If
you followed the instructions above and have been invited to
the [atomist-playground][play-gh] GitHub organization, you will have
been added to this team in that organization.  If you are trying to
run these automations in your own Slack team and GitHub organization,
you will have to create a team in your GitHub organization named
`atomist-automation` and add the users who want to create and register
automations to it.

## Starting up the automation-client

To start the client, run the following command:

```
$ npm run start
```

## Invoking a command handler from Slack

This project contains the code to create and respond to a simple
`search so` bot command.  The code that defines the bot command and
implements responding to the command, i.e., the _command handler_, can
be found in [`SearchStackOverflow.ts`][search].  Once you have your local
automation client running (the previous step in this guide), you can
invoke the command handler by sending the Atomist bot the command in
any channel of your Slack team:

```
@atomist search so q="<some query>"
```

Once you've submitted the command in Slack, you'll see the incoming
and outgoing messages show up in the logs of your locally running
automation-client.  Ultimately, you should see the response from the
bot in Slack.

[search]: https://github.com/atomist-blog/sof-command/blob/master/src/commands/SearchStackOverflow.ts (SearchStackOverflow Command Handler)

Feel free to modify the code in the `SearchStackOverflow` command handler,
restart your local automation client, and see what happens!

## Dashboard and GraphQL data explorer

When the automation client has successfully established a connection
to the Atomist API server, the Dashboard (work-in-progress) and
GraphQL data explorer will be available.

*   Dashboard: http://localhost:2866
*   GraphQL Data Explorer: http://localhost:2866/graphql

## Support

General support questions should be discussed in the `#support`
channel in our community Slack team
at [atomist-community.slack.com][slack].

If you find a problem, please create an [issue][].

[issue]: https://github.com/atomist/automation-seed-ts/issues

## Development

You will need to install [node][] to build and test this project.

### Build and Test

Command | Reason
------- | ------
`npm install` | to install all the required packages
`npm run start` | to start the Atomist automation client
`npm run lint` | to run tslint against the TypeScript
`npm run compile` | to compile all TypeScript into JavaScript
`npm test` | to run tests and ensure everything is working
`npm run autotest` | run tests continuously (you may also need to run `tsc -w`)
`npm run clean` | remove stray compiled JavaScript files and build directory

### Release

To create a new release of the project, simply push a tag of the form
`M.N.P` where `M`, `N`, and `P` are integers that form the next
appropriate [semantic version][semver] for release.  The version in
the package.json is replaced by the build and is totally ignored!  For
example:

[semver]: http://semver.org

```
$ git tag -a 1.2.3
$ git push --tags
```

The Travis CI build (see badge at the top of this page) will publish
the NPM module and automatically create a GitHub release using the tag
name for the release and the comment provided on the annotated tag as
the contents of the release notes.

---

Created by [Atomist][atomist].
Need Help?  [Join our Slack team][slack].

[atomist]: https://www.atomist.com/
[slack]: https://join.atomist.com
