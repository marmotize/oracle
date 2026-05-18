# Marmotize Release

Fork releases are published from `release/marmotize` as `@marmotize/oracle`.

## Local setup

Use Node 24 and the package-manager pin through Corepack:

```sh
nvm use
corepack pnpm install --frozen-lockfile
```

The branch pins `pnpm@11.1.2` and enables pnpm supply-chain checks in
`pnpm-workspace.yaml`.

## First publish bootstrap

npm trusted publishing can only be configured after the package exists on the
registry. For the first `@marmotize/oracle` publish only:

1. Create a short-lived npm granular access token with publish rights.
2. Add it to `marmotize/oracle` as the GitHub Actions secret `NPM_TOKEN`.
3. Rerun the `Marmotize Release` workflow.
4. After the package exists, remove the `NPM_TOKEN` secret.

## npm trusted publisher

After the first publish, configure `@marmotize/oracle` on npmjs.com:

- Publisher: GitHub Actions
- Organization or user: `marmotize`
- Repository: `oracle`
- Workflow filename: `marmotize-release.yml`
- Environment name: leave empty

The workflow then uses OIDC trusted publishing. Do not keep an `NPM_TOKEN` secret
for ongoing publishing.

## Release flow

Create release notes and version changes with:

```sh
corepack pnpm changeset
```

Push to `release/marmotize`. The workflow either opens a release PR or publishes
the ready version to npm.
