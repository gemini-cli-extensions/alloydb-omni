# AlloyDB Omni Agent Skills

> [!NOTE]
> Currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This repository provides a set of agent skills to interact with [AlloyDB Omni](https://docs.cloud.google.com/alloydb/omni/docs) instances. These skills can be used with various AI agents, including [Antigravity](https://antigravity.google/), [Claude Code](https://claude.com/product/claude-code) and [Codex](https://developers.openai.com/codex), to manage your databases, execute queries, explore schemas, and troubleshoot issues using natural language prompts.

> [!IMPORTANT]
> **We Want Your Feedback!**
> Please share your thoughts with us by filling out our feedback [form][form].
> Your input is invaluable and helps us improve the project for everyone.

[form]: https://docs.google.com/forms/d/e/1FAIpQLSfEGmLR46iipyNTgwTmIDJqzkAwDPXxbocpXpUbHXydiN1RTw/viewform?usp=pp_url&entry.157487=alloydb-omni

## Table of Contents

- [Why Use AlloyDB Omni Agent Skills?](#why-use-alloydb-omni-agent-skills)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Configuration](#configuration)
  - [Installation & Usage](#installation--usage)
    - [Antigravity](#antigravity)
    - [Claude Code](#claude-code)
    - [Codex](#codex)
- [Usage Examples](#usage-examples)
- [Supported Skills](#supported-skills)
- [Troubleshooting](#troubleshooting)

## Why Use AlloyDB Omni Agent Skills?

- **Seamless Workflow:** Integrates seamlessly into your AI agent's environment. No need to constantly switch contexts for common database tasks.
- **Natural Language Queries:** Stop wrestling with complex commands. Explore schemas and query data by describing what you want in plain English.
- **Full Lifecycle Control:** Manage the entire lifecycle of your database, from creating clusters to exploring schemas and running queries.
- **Code Generation:** Accelerate development by asking your agent to generate data classes and other code snippets based on your table schemas.

## Prerequisites

Before you begin, ensure you have the following:

- One of these AI agents installed
  - Antigravity
     - [Antigravity CLI](https://github.com/google-gemini/gemini-cli) version **v1.6.0** or higher
     - [Antigravity 2.0](https://antigravity.google/product/antigravity-2) version **v2.0.0** or higher.
  - [Claude Code](https://claude.com/product/claude-code) version **v2.1.94** or higher.
  - [Codex](https://developers.openai.com/codex) **v0.117.0** or higher.
- An active AlloyDB Omni instance.

## Getting Started

### Configuration

Please keep these environment variables handy during the installation process:

*   `ALLOYDB_OMNI_HOST`: (Optional: localhost by default) The host of your AlloyDB cluster.
*   `ALLOYDB_OMNI_PORT`: (Optional: 5432 by default) The port of your AlloyDB cluster.
*   `ALLOYDB_OMNI_DATABASE`: The name of the database to connect to.
*   `ALLOYDB_OMNI_USER`: The database username.
*   `ALLOYDB_OMNI_PASSWORD`: The password for the database user.
*   `ALLOYDB_OMNI_QUERY_PARAMS`: (Optional) Additional query parameters.

### Installation & Usage

To start interacting with your database, install the skills for your preferred AI agent, then launch the agent and use natural language to ask questions or perform tasks.

For the latest version, check the [releases page][releases].

[releases]: https://github.com/gemini-cli-extensions/alloydb-omni/releases

<!-- {x-release-please-start-version} -->

<details open>
<summary id="antigravity">Antigravity</summary>

You can use either of these two agents for Antigravity:
- [Antigravity CLI](https://github.com/google-gemini/gemini-cli) version **v1.6.0** or higher
- [Antigravity 2.0](https://antigravity.google/product/antigravity-2) version **v2.0.0** or higher.

<blockquote>
💡 <strong>Tip — Migrating from Gemini CLI?</strong><br>
If you previously installed this extension with <code>gemini extensions install</code>, you can convert it to an Antigravity plugin instead of reinstalling from scratch:
<ul>
  <li><strong>On first launch of Antigravity CLI</strong>, accept the Migration Options prompt to automatically convert your installed Gemini CLI extensions to Antigravity plugins.</li>
  <li><strong>Or, from your terminal</strong>, run:
    <pre><code class="language-bash">agy plugin import gemini</code></pre>
  </li>
</ul>
See <a href="https://antigravity.google/docs/gcli-migration">Migrating from Gemini CLI</a> for details on plugins, context files (<code>GEMINI.md</code> / <code>AGENTS.md</code>), and MCP server config differences.
</blockquote>

#### Antigravity 2.0 (IDE)

**1. Clone the Repo:**

```bash
git clone --branch 0.2.1 https://github.com/gemini-cli-extensions/alloydb-omni.git
```

**2. Install the skills:**

Choose a location for the skills:
- **Global (all workspaces):** `~/.gemini/antigravity/skills/`
- **Workspace-specific:** `<workspace-root>/.agents/skills/`

Copy the skill folders from the cloned repository's `skills/` directory to your chosen location:

```bash
cp -R alloydb-omni/skills/* ~/.gemini/antigravity/skills/
```

**3. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

_(Tip: Antigravity 2.0 automatically discovers skills in these directories at the start of a session. You can verify they are active by running the `/skills` command in your active session.)_

#### Antigravity CLI

You can install plugins directly from a remote GitHub repository.

**1. Install the plugin:**

```bash
agy plugin install https://github.com/gemini-cli-extensions/alloydb-omni
```

**2. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

</details>

<details>
<summary id="claude-code">Claude Code</summary>

**1. Set env vars:**
In your terminal, set your environment vars as described in the [configuration section](#configuration).

**2. Start the agent:**

```bash
claude
```

**3. Install the plugin:**

```bash
/plugin install alloydb-omni@claude-plugins-official
```

_(Tip: Run `/plugin list` inside Claude Code to verify the plugin is active, or `/reload-plugins` if you just installed it.)_

</details>

<details>
<summary id="codex">Codex</summary>

**1. Install marketplace:**

```bash
codex plugin marketplace add GoogleCloudPlatform/data-agent-kit
```

**2. Install the plugin:**

```bash
codex plugin install alloydb-omni@data-agent-kit
```

**3. Set env vars:**
Enter your environment vars as described in the [configuration section](#configuration).

**4. (Optional) Update the marketplace:**
```sh
codex plugin marketplace upgrade data-agent-kit
```

</details>

## Installing using [open agent skills tool](https://github.com/vercel-labs/skills)

You can install skills using the `npx skills` command.

**1. Install the skills:**

Run the following command in your terminal to automatically download and register the skills:

```bash
npx skills add https://github.com/gemini-cli-extensions/alloydb-omni/tree/0.2.1
```

For detailed info check out the [Skills npm package](https://www.npmjs.com/package/skills).

**2. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

<!-- {x-release-please-end} -->

## Usage Examples

Interact with AlloyDB Omni using natural language right from your IDE:

* **Provision Infrastructure:**
    * "Create a new AlloyDB Omni container with Docker."
    * "Show me all the AlloyDB Omni DBClusters on my Kubernetes cluster."

* **Explore Schemas and Data:**
    * "Show me all tables in the 'orders' database."
    * "What are the columns in the 'products' table?"
    * "How many orders were placed in the last 30 days, and what were the top 5 most purchased items?"

* **Generate Code:**
    * "Generate a Python dataclass to represent the 'customers' table."

## Supported Skills

The following skills are available in this repository:

- [AlloyDB Omni Data](./skills/alloydb-omni-data/SKILL.md) - Use these skills when you need to explore the database structure, identify schema objects like views and triggers, and execute SQL queries to interact with your data.
- [AlloyDB Omni Performance](./skills/alloydb-omni-performance/SKILL.md) - Use these skills when you need to analyze query performance, generate execution plans, check table/column statistics, and monitor overall database activity.
- [AlloyDB Omni Monitor](./skills/alloydb-omni-monitor/SKILL.md) - Use these skills when you need to troubleshoot production issues by identifying locks, tracking long-running transactions, and getting a high-level view of server state.
- [AlloyDB Omni Optimize](./skills/alloydb-omni-optimize/SKILL.md) - Use these skills when you need to fine-tune the database engine settings, manage extensions, or optimize the columnar engine for better analytical performance.
- [AlloyDB Omni Health](./skills/alloydb-omni-health/SKILL.md) - Use these skills when you need to audit database health, identify storage bloat, find broken indexes, and verify tablespace or maintenance configurations.
- [AlloyDB Omni Replication](./skills/alloydb-omni-replication/SKILL.md) - Use these skills when you need to monitor the health of database replication, manage sync states between nodes, and audit publication tables for distributed setups.
- [AlloyDB Omni Access Control](./skills/alloydb-omni-access-control/SKILL.md) - Use these skills when you need to manage user roles, inspect permissions, and verify security-related configuration parameters.
- [AlloyDB Omni Container](./skills/alloydb-omni-container/SKILL.md) - Use these skills to manage AlloyDB Omni in container environments.
- [AlloyDB Omni Kubernetes](./skills/alloydb-omni-kubernetes/SKILL.md) - Use these skills to manage AlloyDB Omni on Kubernetes.

## Troubleshooting

Use the debug mode of your agent (e.g., `gemini --debug`) to enable debugging.

Common issues:

* "✖ Error during discovery for server: MCP error -32000: Connection closed": The database connection has not been established. Ensure your configuration is set via environment variables.
* "✖ MCP ERROR: Error: spawn ... ENOENT": A skill script or dependency might be missing. Ensure you have Node.js installed and have properly installed the extension.

