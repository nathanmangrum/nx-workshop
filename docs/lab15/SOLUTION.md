##### Final CI config

```yml
name: Run CI checks

on: [pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    name: Building affected apps
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - uses: bahmutov/npm-install@v1
      - run: npx nx affected --target=build --base=origin/master --parallel
      - run: npx nx affected --target=test --base=origin/master --parallel
      - run: npx nx affected --target=lint --base=origin/master --parallel
      - run: npx nx affected --target=e2e --base=origin/master --parallel
```

##### Marking all projects as affected

```json
  "implicitDependencies": {
    ".github/workflows/ci.yml": "*",
```
