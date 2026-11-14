<p align="center">
  <a href="https://drums.run">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Drums-Labs/.github/main/profile/assets/drums-symbol-light.svg">
      <img src="https://raw.githubusercontent.com/Drums-Labs/.github/main/profile/assets/drums-symbol.svg" alt="Drums" width="96">
    </picture>
  </a>
</p>

<h1 align="center">Drums</h1>

<p align="center">
  Infrastructure for computer-use RL: hundreds of isolated desktops per server, each one forkable, resettable and verifiable.
</p>

<p align="center">
  <a href="https://drums.run">Website</a> ·
  <a href="https://console.drums.run/docs">Docs</a> ·
  <a href="https://bench.drums.run">Benchmarks</a> ·
  <a href="https://console.drums.run">Console</a> ·
  <a href="https://pypi.org/project/drums-sdk/">PyPI</a>
</p>

## What Drums is

Training a computer-use agent means running the same desktop task thousands of times. Drums runs many isolated
desktops on one Linux host by sharing one running operating system and its applications while keeping each desktop's
mutable state separate. A desktop restores from a template in seconds, forks at any point, resets in well under a
second, and reports a verified reward at the end of a rollout.

## Repositories

| Repository | What it is | Language |
|---|---|---|
| [drumsd](https://github.com/Drums-Labs/drumsd) | The host daemon: desktops, templates, fork, reset, the HTTP API and the installer | Rust, Python |
| [drums-python-sdk](https://github.com/Drums-Labs/drums-python-sdk) | `pip install drums-sdk`: Python client and the `drums mcp` server for agent frameworks | Python |
| [drums-verifiers](https://github.com/Drums-Labs/drums-verifiers) | Environments for [verifiers](https://github.com/PrimeIntellect-ai/verifiers) and prime-rl: OSWorld tasks, a seeded task factory, audited rewards | Python |
| [drums-criu](https://github.com/Drums-Labs/drums-criu) | Our fork of [CRIU](https://criu.org) with the template server and restore-fidelity patches drumsd depends on | C |

## Start here

Hosted, no server needed. Create an API key at [console.drums.run](https://console.drums.run), then:

```bash
pip install drums-sdk
export DRUMS_URL=https://beta.drums.run/gw
export DRUMS_TOKEN=drums_sk_...
```

```python
import drums

with drums.connect() as client:
    with client.create(task="e0df059f", ttl=900) as env:   # an OSWorld task; ttl in seconds
        env.wait_valid()
        env.step("pyautogui.click(960, 540)")
        reward = env.verify(strict=False)
        print("score", reward.score, "valid", reward.valid)
```

Agent frameworks that speak MCP get the same desktops from `drums mcp`; see the
[MCP guide](https://console.drums.run/docs/guides/mcp).

Self-hosted: the [drumsd install guide](https://github.com/Drums-Labs/drumsd/blob/main/docs/install.md) takes a fresh
Ubuntu 24.04 host to a running Drums server.

## Licences

Apache-2.0 for Drums code. drums-criu stays GPL-2.0 like upstream CRIU. Security reports go through each
repository's private vulnerability reporting, see its SECURITY.md.
