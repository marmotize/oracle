# Changesets

This fork release branch uses Changesets to prepare npm releases for `@marmotize/oracle`.

Create a changeset for release-visible changes:

```sh
corepack pnpm changeset
```

The `Marmotize Release` workflow creates a release PR when changesets are present, and publishes when the versioned package is ready.
