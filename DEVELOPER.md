# DEVELOPER.md

This document provides instructions for setting up your development environment and contributing to the AlloyDB Omni Gemini CLI Extension project.

## Prerequisites

Before you begin, ensure you have the following:

1.  **Gemini CLI:** Install the Gemini CLI version v0.6.0 or above. Installation instructions can be found on the official Gemini CLI documentation. You can verify your version by running `gemini --version`.
2.  **Node.js:** Required for running and testing skill scripts locally.
3.  **AlloyDB Omni Instance:** For testing skills, you will need access to an active AlloyDB Omni instance.
4.  For AlloyDB Omni for Kubernetes, you will need to have access to a Kubernetes cluster with AlloyDB Omni operator installed. Instructions can be found on the [AlloyDB Omni for Kubernetes documentation](https://docs.cloud.google.com/alloydb/omni/kubernetes/current/docs/overview).

## Developing the Extension

### Running from Local Source

The development process involves installing the extension locally into the Gemini CLI to test changes.

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/gemini-cli-extensions/alloydb-omni.git
    cd alloydb-omni
    ```

2.  **Install the Extension Locally:** Use the Gemini CLI to install the extension from your local directory.

    ```bash
    gemini extensions link .
    ```
    The CLI will prompt you to confirm the installation. Accept it to proceed.

3.  **Testing Changes:** After installation, start the Gemini CLI (`gemini`). You can now interact with the `alloydb-omni` skills to manually test your changes against your connected database.

    You can also test individual skill scripts directly using Node.js:
    ```bash
    node skills/alloydb-omni-data/scripts/execute_sql.js '{"sql": "SELECT 1"}'
    ```

## Testing

### Automated Presubmit Checks

A GitHub Actions workflow (`.github/workflows/presubmit-tests.yml`) is triggered for every pull request. This workflow primarily verifies that the extension can be successfully installed by the Gemini CLI.

A skills validation workflow (`.github/workflows/skills-validate.yml`) also runs to ensure the integrity of the generated skills.

### Other GitHub Checks

* **License Header Check:** A workflow ensures all necessary files contain the proper license header.
* **Conventional Commits:** This repository uses [Release Please](https://github.com/googleapis/release-please) to manage releases. Your commit messages must adhere to the [Conventional Commits](https://www.conventionalcommits.org/) specification.
* **Dependency Updates:** [Renovate](https://github.com/apps/forking-renovate) is configured to automatically create pull requests for dependency updates.

## Building the Extension

Building this extension is as simple as making sure all files are in the right place. The extension is distributed as a source repository, and users install it by pointing to this repository.

## Maintainer Information

### Team

The primary maintainers for this repository are defined in the [`.github/CODEOWNERS`](.github/CODEOWNERS) file:

* `@gemini-cli-extensions/alloydb-omni-admin`
* `@gemini-cli-extensions/alloydb-omni-maintainers`

### Releasing

The release process is automated using `release-please`.

1.  **Release PR:** When commits with conventional commit headers (e.g., `feat:`, `fix:`) are merged into the `main` branch, `release-please` will automatically create or update a "Release PR".
2.  **Merge Release PR:** A maintainer approves and merges the Release PR. This action triggers `release-please` to create a new GitHub tag and a corresponding GitHub Release.
