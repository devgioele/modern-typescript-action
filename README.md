<p align="center">
  <a href="https://github.com/devgioele/modern-typescript-action"><img alt="modern-typescript-action status" src="https://github.com/devgioele/modern-typescript-action/workflows/Verification/badge.svg"></a>
</p>

# Create a modern GitHub Action

Use this template to bootstrap the creation of a GitHub Action :rocket:

This template includes compilation support, tests, a validation workflow, publishing, and versioning guidance.  

If you are new, there's also a simpler introduction.  See the [Hello World JavaScript Action](https://github.com/actions/hello-world-javascript-action)

## Includes

- [TypeScript](https://www.typescriptlang.org/)
- [ESLint](https://eslint.org/)
- [Prettier](https://prettier.io/)
- [yarn](https://yarnpkg.com/)
- [esbuild](https://esbuild.github.io/)
- [@swc/jest](https://swc.rs/docs/usage/jest)
- [act](https://github.com/nektos/act)
- [VS Code](https://code.visualstudio.com/) settings

## Requirements

- Node.js `16 or higher`

## Create an action from this template

Click the `Use this Template` and provide the new repo details for your action

## Getting started

Install the dependencies  
```bash
$ yarn
```

Install [act](https://github.com/nektos/act) to run GitHub Actions locally, which includes having Docker.

Test, build and run the action
```bash
$ yarn dev
```

## Change action.yml

The action.yml defines the inputs and output for your action.

Update the action.yml with your name, description, inputs and outputs for your action.

See the [documentation](https://help.github.com/en/articles/metadata-syntax-for-github-actions)

## Change the Code

Most toolkit and CI/CD operations involve async operations so the action is run in an async function.

```javascript
import * as core from '@actions/core';
...

async function run() {
  try { 
      ...
  } 
  catch (error) {
    core.setFailed(error.message);
  }
}

run()
```

See the [toolkit documentation](https://github.com/actions/toolkit/blob/master/README.md#packages) for the various packages.

## Publish to a distribution branch

Actions are run from GitHub repos so we will checkin the packed dist folder. 

Then run [ncc](https://github.com/zeit/ncc) and push the results:
```bash
$ npm run package
$ git add dist
$ git commit -a -m "prod dependencies"
$ git push origin releases/v1
```

Your action is now published! :rocket: 

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)

## Validate

You can now validate the action by referencing `./` in a workflow in your repo (see [test.yml](.github/workflows/test.yml))

```yaml
uses: ./
with:
  milliseconds: 1000
```

See the [actions tab](https://github.com/actions/typescript-action/actions) for runs of this action! :rocket:

## Usage

After testing you can [create a v1 tag](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md) to reference the stable and latest V1 action

## Debugging

`core.debug()` does only output if the debugging mode is enabled.

On **GitHub** you can enable it by setting the **secret** `ACTIONS_STEP_DEBUG` to `true`.
\_Note: You should hesitate to enable this on GitHub, because secrets may be printed while in debug mode.

If using **act**, you can enable it by passing the flag `--verbose`.
_Note: This does not currently work. Follow [the related GitHub issue](https://github.com/nektos/act/issues/1006)._

## Using secrets locally

The `.secrets` file is a [.env](https://www.dotenv.org/env) file placed in the root directory that is used to pass secrets to the GitHub Action while running it locally with act.