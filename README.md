# mocker-nodejs
Docker emulated Cloud Foundry nodejs Buildpack

## Description

This docker image will try to emulate Cloud Foundry runtime for the [Nodejs Buildpack](https://github.com/cloudfoundry/nodejs-buildpack). It is based on the new Cloud Foundry Stack - [cflinuxfs2](https://github.com/cloudfoundry/stacks) which is based upon Ubuntu 14.04.

> **WARNING: [cf-release v204](https://groups.google.com/a/cloudfoundry.org/forum/#!topic/vcap-dev/gU7rpD8MSC4)** was the first release to support cflinuxfs2 stack. Buildpacks prior to this cf-release version could not work.

## Configuration
This image has a few env vars that you can modify to alter the behavior at runtime. But the 3 more important are:
* **RUN_COMMAND**: This is the command to run your app. For most java apps this defaults to what `bin/expose` script creates. ***Required***
* **BP_URL**: This is the java buildpack git url. This is mainly intended for custom java buildpacks. `default: https://github.com/cloudfoundry/nodejs-buildpack.git`
* **BP_VERSION**: This is the version of the buildpack to checkout. `default: v1.2.1`

> Two important thing to know is that ***you must mount your code in the /object path of the image*** and ***Default listening port is 8080 (Remember to expose it)***, you can check the next examples to see how to do this.-

## Usage
```bash
$ git clone https://github.com/heroku/node-js-sample.git $HOME/workspace/node-js-sample
$ docker run -p 8080:8080 -e RUN_COMMAND="npm start" -v $HOME/workspace/node-js-sample:/object cacciald/mocker-nodejs:latest
```

> For a more advanced deployment I can recommend you to use [fig/docker compose](https://docs.docker.com/compose/).-
