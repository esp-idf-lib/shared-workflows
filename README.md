# esp-idf-lib/shared-workflows

This repository contains shared workflows for `esp-idf-lib`. All the workflows
are reusable workflows, meaning, they are supposed to be called by other
workflows.

Here is an example to call `do-something.yml` from other repositories.

```yaml
---
name: Do something
on: push
jobs:
  publish:
    uses: esp-idf-lib/shared-workflows/.github/workflows/do-something.yml@main
```

> [!NOTE]
> Specify `@main` as the workflow version. This ensures all the components use
> the latest workflows.

<!-- vim-markdown-toc GFM -->

* [Workflows](#workflows)
    * [build-docs.yml](#build-docsyml)
    * [build-examples.yml](#build-examplesyml)
    * [publish-esp-component-registry.yml](#publish-esp-component-registryyml)
    * [validate-astyle.yml](#validate-astyleyml)
    * [validate-component.yml](#validate-componentyml)
    * [validate-with-esp-component-registry.yml](#validate-with-esp-component-registryyml)

<!-- vim-markdown-toc -->

## Workflows

These workflows are enabled by default when a repository is created from
[esp-idf-lib/template-component](https://github.com/esp-idf-lib/template-component).

### build-docs.yml

The workflow builds the docs and, optionally, publishes the HTML files to GitHub
Pages. It needs additional permissions.

```yaml
---
name: Publish HTML files on GitHub Pages
on: release
permissions:
  # required by actions/deploy-pages
  pages: write
  id-token: write
jobs:
  publish:
    uses: esp-idf-lib/shared-workflows/.github/workflows/build-docs.yml@main
    with:
      publish: true
```

### build-examples.yml

The workflow builds all the examples under `examples`.

### publish-esp-component-registry.yml

The workflow publishes the component to ESP Component Registry. An input,
`components` is required. See
[the workflow](.github/workflows/publish-esp-component-registry.yml) for more
details.

> [!NOTE]
> The workflows uses
> [espressif/upload-components-ci-action](https://github.com/espressif/upload-components-ci-action)
> internally. The GitHub Action needs an ESP Component Registry Token. Because
> the token is set at the organization level (`ESP_TOKEN`) as a secret. No token is
> required when you call this workflow.

### validate-astyle.yml

The workflow validates code style.

### validate-component.yml

The workflow validates a component. The rules are written in Ruby RSpec. See
[spec](https://github.com/esp-idf-lib/validate-esp-idf-lib-component/tree/main/spec)
directory for more details about the rules.

### validate-with-esp-component-registry.yml

The workflow validates a component with ESP Component Registry's API.
