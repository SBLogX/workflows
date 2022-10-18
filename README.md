# Upply Workflows

## Deploy

*TODO*

## Gitflow

Reusable workflows are available to follow the [Gitflow](https://www.notion.so/upply-project/Gitflow-60a5c54297b6403a9a99b792f975c26f).
To use those workflows, you have to create 4 workflows in your repository:

<details>
  <summary>See workflows</summary>

`.gitflow/workflows/release.yml`:
```yaml
name: Release
on:
  push:
    branches:
      - release/*

jobs:
  release:
    name: Release
    uses: SBLogX/workflows/.github/workflows/gitflow-release.yml@main
    secrets: inherit
```

`.gitflow/workflows/release-merged.yml`:
```yaml
name: Release merged
on:
  pull_request:
    types:
      - closed
    branches:
      - main

jobs:
  release_merged:
    name: Release merged
    uses: SBLogX/workflows/.github/workflows/gitflow-release-merged.yml@main
    if: github.event.pull_request.merged == true && startsWith(github.head_ref, 'release/')
    secrets: inherit
```

`.gitflow/workflows/hotfix.yml`:
```yaml
name: Hotfix
on:
  push:
    branches:
      - hotfix/*

jobs:
  hotfix:
    name: Hotfix
    uses: SBLogX/workflows/.github/workflows/gitflow-hotfix.yml@main
    secrets: inherit
```

`.gitflow/workflows/hotfix-merged.yml`:
```yaml
name: Hotfix merged
on:
  pull_request:
    types:
      - closed
    branches:
      - main

jobs:
  hotfix_merged:
    name: Hotfix merged
    uses: SBLogX/workflows/.github/workflows/gitflow-hotfix-merged.yml@main
    if: github.event.pull_request.merged == true && startsWith(github.head_ref, 'hotfix/')
    secrets: inherit
```

</details>

### Features

It will do for you:

#### Release process:

- Create pull requests for new `release/*` branches
- Create release candidate `X.X.X-rc.x` after each push
- Sync `develop` branch after merge
- Create final release after merge
- Delete release branch after merge

#### Hotfix process:

- Create pull requests for new `hotfix/*` branches
- Create release candidate `X.X.X-hf.x` after each push
- Sync `develop` branch and all `release/*` branch after merge
- Create final release after merge
- Delete hotfix branch after merge

## Pact

*TODO*
