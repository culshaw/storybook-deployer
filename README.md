# YunoJuno Storybook Deployer

This is a simple tool allows you to deploy your Storybook into Github Pages.
It relies on a fully qualified github url (username + token) set in an environment variable with the repositry to deploy to.
This is useful for services like Heroku if you are building the storybook as part of the buildpack.

## Getting Started

Install Storybook Deployer with:

```
npm i --save @kadira/storybook-deployer
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

