# Mastering GitHub Actions: Advanced Event Filtering

## 1. Branch Filters
Use `branches` and `branches-ignore` to control which branches trigger workflows.

```yaml
on:
  push:
    branches:
      - main
      - dev
    branches-ignore:
      - 'feature/*'
```
## 2. Path Filters
Path filters let you run workflows only when certain files or directories change,Example: Run workflow only if files in src/ are modified:

```yaml
on:
  push:
    branches:
      - main
    paths:
      - 'src/**'
```
Variations:

```yaml
on:
  push:
    paths:
      - 'src/*'        # only top-level files in src/
      - 'src/**'       # all files & subfolders in src/
      - '**.md'        # any Markdown file in repo
      - '!docs/**'     # exclude docs folder
```

Combine with Branches

```yaml
on:
  push:
    branches:
      - main
    paths:
      - 'src/**'
    paths-ignore:
      - 'src/test/**'
```

## 3. Type Filters
Types filters let you control which sub-events of an event trigger the workflow.For example, a pull_request event can fire for many actions:

Opened, Reopened, Synchronized (new commits added), Closed, Labeled, Assigned
…and more.

You can filter which ones actually trigger the workflow:

```yaml
on:
  pull_request:
    types: [opened, reopened, synchronize]
```
Combine with Branch & Path Filters

You can combine everything together:
```yaml
on:
  pull_request:
    branches:
      - main
    paths:
      - 'src/**'
    types: [opened, synchronize]
```


