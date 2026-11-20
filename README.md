# octiq-cifx-J7-jenkins-commented-out

A small Node.js project used as a CI detection fixture. It exists to verify that
test detection ignores `npm test` occurrences that appear only inside comments.

## What's here

- `package.json` — private `fixture` package with two scripts: `build`
  (`echo building`) and `test` (`node test.js`).
- `test.js` — a trivial test runner that exits non-zero if `1 + 1 !== 2` and
  otherwise prints `1 passing`.
- `Jenkinsfile` — declarative pipeline with a single `Build` stage.

## Tests

The project does have real tests: `npm test` runs `node test.js`, which prints
`1 passing` on success.

However, this is deliberately a fixture for comment handling. In the
`Jenkinsfile`, the only references to `npm test` are commented out:

```groovy
// sh 'npm test'
/* sh 'npm run test:ci' */
sh 'npm run build'
```

Because those test commands live inside `//` and `/* */` comments, the CI
detection should **not** count them. The expected verdict is anything except
"Tests required" — i.e. `Tests not required` — even though a real
`test` script exists in `package.json`.

## Fixture purpose

This repository represents the "Jenkins commented-out test" scenario: the
pipeline appears to run tests at a glance, but all such steps are comments, so
the only executed command is `npm run build`. The `Jenkinsfile` and code are
intentionally left as-is; they are the fixture under test.
