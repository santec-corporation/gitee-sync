# Sync to Gitee

This public repository provides a reusable **GitHub Actions workflow** for synchronizing repositories from the **GitHub organization `santec-corporation`** to their mirrored counterparts in **Gitee (`santec-corporation-cn`)**.

> ⚠️ **Important:** This repository **must remain public**, otherwise other public repositories will be unable to reference its workflow using `uses:` syntax.

---

## 📘 Overview

This workflow allows developers to easily mirror a GitHub repository to Gitee by pushing all branches and tags. It supports both manual triggering (`workflow_dispatch`) and programmatic invocation (`workflow_call`) from other repositories.

The workflow ensures that the Gitee mirror stays perfectly in sync with the source repository by force-pushing all branches and tags.

---

## ⚙️ Usage

### 1. Reference this workflow in another repository

In your repository (e.g., `santec-corporation/ExampleRepo`), create a workflow file such as `.github/workflows/sync-to-gitee.yml`:

```yaml
name: Sync to Gitee

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  call-sync:
    uses: santec-corporation/sync-to-gitee/.github/workflows/sync.yml@main
    with:
      repo-name: ExampleRepo
```

This calls the reusable workflow from this public repository.

---

### 2. Provide required secrets and variables

Ensure the following are configured in your GitHub repository settings:

* **Secrets → `GITEE_PAT`** – Your Gitee Personal Access Token with `repo` permissions.
* **Variables → `GITEE_USERNAME`** – Your Gitee username.

---

### 3. Triggering the sync

You can trigger the sync:

* **Automatically** – whenever a new push is made to your repository (if configured).
* **Manually** – via the GitHub Actions tab → *Run workflow*.
* **Programmatically** – by invoking it through another workflow using `workflow_call`.

---

## 🧩 Notes

* This workflow **must remain public** to be reusable across public repositories.
* It assumes a one-to-one mirror structure between `santec-corporation` (GitHub) and `santec-corporation-cn` (Gitee).
* The sync process uses `--force` to ensure a perfect mirror. Use with caution if manual commits exist in the Gitee repo.

---

## 🪪 License

This repository and workflow are provided under the MIT License. See [LICENSE](./LICENSE) for details.
