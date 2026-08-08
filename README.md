<p align="center">
  <img src="docs/logo.svg" alt="Inx" width="640"/>
</p>

<p align="center">
  <strong>English</strong>
  &nbsp;·&nbsp;
  <a href="./README.zh-CN.md">简体中文</a>
  &nbsp;·&nbsp;
  <a href="./docs/GUIDE.md">Guide</a>
  &nbsp;·&nbsp;
  <a href="./docs/ACP.md">ACP</a>
  &nbsp;·&nbsp;
  <a href="./docs/EXTENSIONS.md">Extensions</a>
  &nbsp;·&nbsp;
  <a href="./docs/SPEC.md">Spec</a>
  &nbsp;·&nbsp;
  <a href="https://esengine.github.io/DeepSeek-Inx/">Website</a>
  &nbsp;·&nbsp;
  <strong><a href="https://discord.gg/XF78rEME2D">Discord</a></strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/inx"><img src="https://img.shields.io/npm/v/inx.svg?style=flat-square&color=cb3837&labelColor=161b22&logo=npm&logoColor=white" alt="npm version"/></a>
  <a href="https://github.com/esengine/DeepSeek-Inx/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/esengine/DeepSeek-Inx/ci.yml?style=flat-square&label=ci&labelColor=161b22&logo=githubactions&logoColor=white" alt="CI"/></a>
  <a href="./LICENSE"><img src="https://img.shields.io/npm/l/inx.svg?style=flat-square&color=8b949e&labelColor=161b22" alt="license"/></a>
  <a href="https://www.npmjs.com/package/inx"><img src="https://img.shields.io/npm/dm/inx.svg?style=flat-square&color=3fb950&labelColor=161b22&label=downloads" alt="downloads"/></a>
  <a href="https://github.com/esengine/DeepSeek-Inx/stargazers"><img src="https://img.shields.io/github/stars/esengine/DeepSeek-Inx.svg?style=flat-square&color=dbab09&labelColor=161b22&logo=github&logoColor=white" alt="GitHub stars"/></a>
  <a href="https://atomgit.com/esengine/DeepSeek-Inx"><img src="https://atomgit.com/esengine/DeepSeek-Inx/star/badge.svg" alt="AtomGit stars"/></a>
  <a href="https://github.com/esengine/DeepSeek-Inx/graphs/contributors"><img src="https://img.shields.io/github/contributors/esengine/DeepSeek-Inx.svg?style=flat-square&color=bc8cff&labelColor=161b22&logo=github&logoColor=white" alt="contributors"/></a>
  <a href="https://github.com/esengine/DeepSeek-Inx/discussions"><img src="https://img.shields.io/github/discussions/esengine/DeepSeek-Inx.svg?style=flat-square&color=58a6ff&labelColor=161b22&logo=github&logoColor=white" alt="Discussions"/></a>
  <a href="https://discord.gg/XF78rEME2D"><img src="https://img.shields.io/badge/discord-join-5865F2.svg?style=flat-square&labelColor=161b22&logo=discord&logoColor=white" alt="Discord"/></a>
</p>

<p align="center">
  <a href="https://trendshift.io/repositories/27020?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-27020" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/repositories/27020/monthly?language=Go" alt="esengine/DeepSeek-Inx | Trendshift" width="250" height="55"/></a>
  <a href="https://trendshift.io/repositories/27020?utm_source=repository-badge&amp;utm_medium=badge&amp;utm_campaign=badge-repository-27020" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/repositories/27020" alt="esengine/DeepSeek-Inx | Trendshift" width="250" height="55"/></a>
</p>

<br/>

<h3 align="center">A DeepSeek-native AI coding agent for your terminal.</h3>
<p align="center">A config- and plugin-driven harness — a single static Go binary, tuned around DeepSeek's prefix cache so token costs stay low across long sessions.</p>

<br/>

> [!IMPORTANT]
> **Community · 加入社区** — bilingual Discord for setup help (`#help` / `#求助`), workflow showcases, and feature ideas. → **<https://discord.gg/XF78rEME2D>**

<br/>

## Features

- **Config-driven.** Providers, the agent, enabled tools, and plugins are all
  declared in `inx.toml`. No hardcoded models.
- **Multi-model & composable.** DeepSeek ships as a preset; any
  OpenAI-compatible endpoint is a config entry, not new code. Optionally run
  two models together (executor + planner) in separate, cache-stable sessions.
- **Plugin-driven.** MCP servers contribute tools, prompts, and resources;
  Extension Protocol v1 sidecars can also intercept runtime events, contribute
  Providers and structured UI, and ship versioned plugin packages.
- **Cache-aware context maintenance.** Startup injects a small stable environment
  summary, stale tool output is snipped/pruned before summary compaction, and the
  built-in tool schema contract is documented for regression review.
- **Zero-friction distribution.** `CGO_ENABLED=0` single binary; cross-compile
  to six targets with one command. The result is a fully self-contained static
  binary — nothing to install on the target machine beyond the binary itself.

## Install

Choose the path that matches how you want to use Inx. The CLI/TUI,
desktop app, and VS Code extension all use the same local Inx engine.

### Path A: CLI / TUI

Install the native binary through npm on any supported platform, or use
Homebrew on macOS:

```sh
npm i -g inx                  # any OS; pulls the prebuilt native binary
brew install esengine/inx/inx   # macOS
```

Prebuilt archives (`darwin|linux|windows × amd64|arm64`) and `SHA256SUMS` are on
every [GitHub release](https://github.com/esengine/DeepSeek-Inx/releases).

### Path B: Desktop app

Use the [official download page](https://inx.io/?download=desktop#start)
for the latest desktop build.

| Platform | Package | Architecture |
| --- | --- | --- |
| macOS | Universal `.dmg` or `.zip` | Apple Silicon / Intel |
| Windows | Installer `.exe` or portable `.zip` | x64 / ARM64 |
| Linux | `.deb` or `.tar.gz` | x64 |

Windows installers are code-signed through [SignPath.io](https://signpath.io/)
with a free certificate provided by the [SignPath Foundation](https://signpath.org/).

### Path C: VS Code extension

Complete Path A first. The extension does not bundle the CLI; it starts your
local `inx acp` backend and adds native chat, editor context, tool-call
approvals, model selection, and workspace sessions.

- **VS Code:** [install from Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=SivanLiu.inx-agent)
- **VSCodium / Eclipse Theia:** [install from Open VSX Registry](https://open-vsx.org/extension/SivanLiu/inx-agent)
- **Extension ID:** `SivanLiu.inx-agent` · [source and usage guide](https://github.com/SivanCola/inx-vscode)

### Path D: Build from source

```sh
git clone https://github.com/esengine/DeepSeek-Inx.git
cd DeepSeek-Inx
make build      # -> bin/inx(.exe)
make cross      # -> dist/ (darwin|linux|windows × amd64|arm64)
```

## Quick start

### CLI / TUI

These commands are for the CLI/TUI installed through Path A:

```sh
inx setup                      # configure a provider and model
inx                            # start an interactive session
inx run "implement the TODOs in main.go"
```

In an interactive session, run `/init` when you want Inx to create project
instructions.

### Desktop app

Download the installer for your platform from the
[official download page](https://inx.io/?download=desktop#start), install
and launch Inx, then configure a provider and model in the app. The CLI
commands above are not required for the desktop app.

For advanced CLI usage and configuration, see the **[CLI reference](./docs/CLI.md)**,
**[Guide](./docs/GUIDE.md)**, and
**[configuration paths](./docs/CONFIG_PATHS.md)**.

## Documentation

- **Getting started:** [Guide](./docs/GUIDE.md) · [CLI reference](./docs/CLI.md) ·
  [Configuration paths](./docs/CONFIG_PATHS.md) · [ACP editor integration](./docs/ACP.md)
- **Features & troubleshooting:** [Subagent profiles](./docs/SUBAGENT_PROFILES.md) ·
  [Context Engine v2](./docs/SESSION_MEMORY_RETRIEVAL.md) ·
  [Capability diagnostics](./docs/CAPABILITY_DIAGNOSTICS.md) ·
  [Recovery and updates](./docs/RECOVERY.md) · [Bot guide](./docs/BOT_GUIDE.md) ·
  [Checkpoints & rewind](./docs/CHECKPOINTS.md)
- **Engineering & migration:** [Spec](./docs/SPEC.md) ·
  [Task contracts & pause policy](./docs/TASK_CONTRACT.md) ·
  [Tool contract](./docs/TOOL_CONTRACT.md) · [Migrating from 0.x](./docs/MIGRATING.md)
- **Extension development:** [Extensions](./docs/EXTENSIONS.md) ·
  [Plugin packages and Manifest v1](./docs/PLUGIN_PACKAGES.md) ·
  [Extension Protocol](./docs/EXTENSION_PROTOCOL.md) ·
  [Go SDK and starter](./sdk/go/README.md)

## Star History

<a href="https://www.star-history.com/?repos=esengine%2FDeepSeek-Inx&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/esengine/DeepSeek-Inx/star-history/assets/star-history/star-history-dark.svg" />
   <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/esengine/DeepSeek-Inx/star-history/assets/star-history/star-history-light.svg" />
   <img alt="Star History Chart" src="https://raw.githubusercontent.com/esengine/DeepSeek-Inx/star-history/assets/star-history/star-history-light.svg" />
 </picture>
</a>

<br/>

## Acknowledgments

A small list of folks whose work has shaped Inx the most — the current top
20 contributors by commit count. The full contributor graph is on
[GitHub](https://github.com/esengine/DeepSeek-Inx/graphs/contributors?all=1).

<!-- inx-top-contributors:start -->
| Contributor | Contributor | Contributor | Contributor |
| --- | --- | --- | --- |
| [**SivanCola**](https://github.com/SivanCola) | [**esengine**](https://github.com/esengine) | [**ttmouse**](https://github.com/ttmouse) | [**lifu963**](https://github.com/lifu963) |
| **inx** (anonymous) | [**HUQIANTAO**](https://github.com/HUQIANTAO) | [**GTC2080**](https://github.com/GTC2080) | [**light-front-theory**](https://github.com/light-front-theory) |
| **merge-order-check** (anonymous) | [**Li-Charles-One**](https://github.com/Li-Charles-One) | [**eghrhegpe**](https://github.com/eghrhegpe) | **wufengfan** (anonymous) |
| [**CVEngineer66**](https://github.com/CVEngineer66) | [**dependabot\[bot\]**](https://github.com/apps/dependabot) | [**lanshi17**](https://github.com/lanshi17) | [**SuMuxi66**](https://github.com/SuMuxi66) |
| [**CnsMaple**](https://github.com/CnsMaple) | [**cyq1017**](https://github.com/cyq1017) | [**JesonChou**](https://github.com/JesonChou) | [**XTLine**](https://github.com/XTLine) |
<!-- inx-top-contributors:end -->

Also a separate thank-you to [**Bernardxu123**](https://github.com/Bernardxu123)
for designing the project logo, and to
[AIGC Link](https://xhslink.com/m/80ngts127cA) for promoting the project on XiaoHongShu.

<p align="center">
  <a href="https://github.com/esengine/DeepSeek-Inx/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=esengine/DeepSeek-Inx&max=100&columns=12" alt="Contributors to esengine/DeepSeek-Inx" width="860"/>
  </a>
</p>

<br/>

---

<p align="center">
  <sub>MIT — see <a href="./LICENSE">LICENSE</a></sub>
  <br/>
  <sub>Built by the community at <a href="https://github.com/esengine/DeepSeek-Inx/graphs/contributors">esengine/DeepSeek-Inx</a></sub>
</p>

---

<p align="center"><sub><strong>Support this project</strong></sub></p>

If Inx has been useful and you'd like to say thanks, you can. It stays a
coffee, not a contract — donations don't buy feature priority or change how
issues get triaged.

- **International** — PayPal: [paypal.me/yuhuahui](https://paypal.me/yuhuahui)
- **国内** — 微信支付（扫码）

<p align="center">
  <img src=".github/sponsor/wechat-pay.jpg" alt="WeChat Pay QR code" width="180"/>
</p>
