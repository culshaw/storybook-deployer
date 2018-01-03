# YunoJuno Storybook Deployer

This is a simple tool allows you to deploy your Storybook into Github Pages.
It relies on a fully qualified github url (username + token) set in an environment variable with the repositry to deploy to.
This is useful for services like Heroku if you are building the storybook as part of the buildpack.

## Getting Started

Install Storybook Deployer with:

```
npm i @storybook/storybook-deployer --save-dev
```
Then add a NPM script like this:

```js
{
  "scripts": {
    ...
    "deploy-storybook": "storybook-to-ghpages",
    ...
  }
}
```

Then you can run `npm run deploy-storybook` to deploy the Storybook to GitHub Pages.

### Custom Build Configuration

If you customize the build configuration with some additional params (like static file directory), then you need to expose another NPM script like this:

```js
{
  "scripts": {
    ...
    "build-storybook": "build-storybook -s public -o .out",
    ...
  }
}
```

> Make sure to set the output directory as **`.out`**.

### Skip Build Step

If you have previously built your storybook output (through a different CI step, etc) and just need to publish it, specify the directory with like this:

```js
 npm run deploy-storybook -- --existing-output-dir=.out
```

### Custom deploy configuration

If you want to customize Git username, email or commit message, add this to `package.json`:

```json
"storybook-deployer": {
  "gitUsername": "Custom Username",
  "gitEmail": "custom@email.com",
  "commitMessage": "Deploy Storybook [skip ci]"
}
```

It will override the default configuration:

```js
"storybook-deployer": {
  "gitUsername": "GH Pages Bot",
  "gitEmail": "hello@ghbot.com",
  "commitMessage": "Deploy Storybook to GitHub Pages"
}
```

To deploy Storybook to a remote other than `origin`, pass a `--remote` flag to `npm run deploy-storybook`.  
For example, to deploy to your `upstream` remote:

```
npm run deploy-storybook -- --remote=upstream
```
 
 Or, to specify a target branch and serve your storybook with rawgit instead of gh-pages:
 ```
 npm run deploy-storybook -- --branch=feature-branch
 ```

Or, to specify a source branch other than `master`, pass a `--source-branch` flag to `npm run deploy-storybook`:
```
npm run deploy-storybook -- --source-branch=release
```
