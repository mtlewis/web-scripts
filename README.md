# web-scripts

[![Build Status](https://travis-ci.com/spotify/web-scripts.svg?branch=master)](https://travis-ci.com/spotify/web-scripts)

A collection of base configs and CLI wrappers used to speed up development @ Spotify.

## About this project

### web-scripts CLI

[@spotify/web-scripts](./packages/web-scripts) is a CLI that combines shared configuration for linting, formatting, testing, building, and shipping libraries for Node and the browser. It is opinionated, but allows configuration to avoid lock-in. You can also pick and choose which scripts you use. It is inspired by other tooling bundles like [react-scripts](https://www.npmjs.com/package/react-scripts) and [kcd-scripts](https://www.npmjs.com/package/kcd-scripts).

```bash
yarn add --dev @spotify/web-scripts husky
```

It is intended to be used within a project as a series of npm scripts.

```json
{
  "devDependencies": {
    "@spotify/web-scripts": "^1.0.0",
    "husky": "^2.5.0"
  },
  "scripts": {
    "build": "web-scripts build",
    "test": "web-scripts test",
    "lint": "web-scripts lint",
    "commit": "web-scripts commit",
    "release": "web-scripts release"
  },
  "husky": {
    "hooks": {
      "pre-commit": "web-scripts precommit",
      "commit-msg": "web-scripts commitmsg"
    }
  }
}
```

View the [full CLI documentation](./packages/web-scripts) for more details on how to get started.

### Spotify shared configurations

The other five projects in this repo are shared configurations for common tools we use for building, linting, and formatting our code. They can be installed separately and used by anyone should they opt to follow our standards. We have a [specialized point-of-view on what belongs in our configs](#methodology). They are all used by the web-scripts CLI by default.

- [@spotify/eslint-config-base](./packages/eslint-config-base)
- [@spotify/eslint-config-react](./packages/eslint-config-react)
- [@spotify/eslint-config-typescript](./packages/eslint-config-typescript)
- [@spotify/prettier-config](./packages/prettier-config)
- [@spotify/tsconfig](./packages/tsconfig)

## Methodology

We have a few guiding principles for this project.

1. Style rules should be auto-fixable and if you can, errors should be linted ahead of runtime.
2. Avoid enforcing code style in static analysis; search for bugs with static analysis, and let auto-formatting deal with code style.
3. Push "fast" checks as far left as you can. Optimize for code editors/IDEs fixing issues and enforcing things; write Git hooks that catch things as a failsafe; and use static analysis in CI to prevent bad things from getting into master.
4. `web-scripts` is meant to be configurable. We want to avoid the "eject" problem. You should be able to easily take the base configs and extend them in your project.

## Related projects we use

- [TypeScript]: a superset of JavaScript which we think helps make code readable and less bug-prone.
- [ESLint]: used for static code analysis with some auto-fixing.
- [Prettier]: use to format code pre-commit and automatically in your editor.
- [Jest]: our preferred JavaScript test framework.
- [husky]: allows us to hook into git events in a convenient way.
- [lint-staged]: allows us to write pre-commit hooks which target specific paths and run a series of commands.

## Contributing

This project adheres to the [Open Code of Conduct][code-of-conduct]. By participating, you are expected to honor this code.

This project is an opinionated approach to static analysis, code formatting, testing, and publishing. It's
the result of consensus between many web engineers inside Spotify, and the default configs will mostly be
written by Spotify employees. _We may reject PRs to the ESLint config if we don't agree that the rule
makes sense as part of our baseline, for example._ Use it if it aligns with your needs!

[eslint]: https://eslint.org/
[typescript]: https://www.typescriptlang.org/
[prettier]: https://prettier.io/
[jest]: https://jestjs.io/
[husky]: https://github.com/typicode/husky
[lint-staged]: https://github.com/okonet/lint-staged
[code-of-conduct]: https://github.com/spotify/code-of-conduct/blob/master/code-of-conduct.md

## Releasing

For now, we will release this repo manually with fixed versions. To do that, use `lerna publish --conventional-commits`.
