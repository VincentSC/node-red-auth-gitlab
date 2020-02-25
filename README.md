# Node-RED Authentication with Gitlab

[Node-RED](https://nodered.org) plugin for authenticating users with Twitter.

This module lets you restrict access to the Node-RED editor to specific Gitlab users. It depends on [passport-gitlab2](http://www.passportjs.org/packages/passport-gitlab2/).


**Note:** this requires Node-RED 0.17 or later

Forked from [node-red-auth-twitter](https://github.com/node-red/node-red-auth-twitter). Kuddos to `knolleary`!

## Install

In your Node-RED user directory, typically `~/.node-red`:

    $ npm install vincentsc/node-red-auth-gitlab

## Usage

### Create a new Gitlab application

To enable access control with Gitlab, you must first create a new application on your Gitlab account. 

Once created, you will be provided a _clientID_ and _clientSecret_ that you will need to use to configure the authentication plugin.

### Configure `adminAuth`

Access control for the Node-RED editor is configured in your `settings.js` file
using the `adminAuth` property.

    adminAuth: require('node-red-auth-gitlab')({
        clientID: GITLAB_APP_ID,
        clientSecret: GITLAB_APP_SECRET,
        baseURL: "http://localhost:1880/",
        gitlabURL: "https://gitlab.com/",
        users: [
           { username: "vincent",permissions: ["*"]}
        ]
    })

The `baseURL` property is the URL used to access the Node-RED editor. The `gitlabURL` is where Gitlab is hosted, defaulting to "https://gitlab.com/".

The `users` property is the list of Gitlab users who are allowed to access the
editor. It is the same as used by `adminAuth` as described in the [security documentation](http://nodered.org/docs/security), but without the `password` property.

A default user can be specified by adding a `default` property to the options object:

        users: [
           ...
        ],
        default: {
            permissions: "read"
        }

## Copyright and license

Copyright JS Foundation and other contributors, http://js.foundation under [the Apache 2.0 license](LICENSE).
