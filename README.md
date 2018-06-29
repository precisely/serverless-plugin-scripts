# Precise.ly fork information

Precise.ly maintains a fork of [serverless-plugin-scripts](https://github.com/mvila/serverless-plugin-scripts) because the upstream version does not inject `serverless.yml` environment variables into the environment of the scripts. The maintainer [is not interested in changing this behavior](https://github.com/mvila/serverless-plugin-scripts/pull/6), but our infrastructure setup relies on it.

To make a release:
- run `yarn compile`
- run `yarn pack`, make sure the generated tarball looks reasonable
- go to the [GitHub release panel](https://github.com/precisely/serverless-plugin-scripts/releases), make a new release, and be sure to upload the tarball with a reasonable name
- make a note of the URL of the tarball in the release
- update dependent packages as needed

---

Original README follows:

---

# serverless-plugin-scripts [![npm version](https://img.shields.io/npm/v/serverless-plugin-scripts.svg)](https://www.npmjs.com/package/serverless-plugin-scripts)

Add scripting capabilities to the [Serverless Framework](https://serverless.com/framework/).

## Installation

Install the plugin in your Serverless (v1.0 or higher) project:

```
npm install --save serverless-plugin-scripts
```

And activate it by adding the following configuration to your `serverless.yml` file:

```yaml
plugins:
  - serverless-plugin-scripts
```

## Usage

### Custom commands

To add a custom command to the Serverless CLI, just define a `custom.scripts.commands` property in your `serverless.yml` file:

```yaml
custom:
  scripts:
    commands:
      hello: echo Hello from ${self:service} service!
```

You can now run `serverless hello` to execute the `hello` command.

### Simple hooks

It is possible to define simple hooks for existing Serverless CLI commands by adding a `custom.scripts.hooks` property in your `serverless.yml` file:

```yaml
custom:
  scripts:
    hooks:
      'deploy:createDeploymentArtifacts': npm run compile
```

The next time you run `serverless deploy`, your script will be automatically invoked during the `deploy:createDeploymentArtifacts` lifecycle event.

To find out about existing lifecycle events, check out [this page](https://gist.github.com/HyperBrain/50d38027a8f57778d5b0f135d80ea406).

## Author

Created and maintained by [Manuel Vila](https://github.com/mvila).

## License

MIT
