<!--
  Orion Belt: GitHub organization profile
  Repo: orion-belt-dev/.github
  Path: profile/README.md, shown on https://github.com/orion-belt-dev
  Hero art: profile/assets/hero-{dark,light}.svg. Edit the dark file, then
  regenerate the light one by swapping the colour classes in its <style>.
-->

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/orion-belt-dev/.github/main/profile/assets/hero-dark.svg">
  <img alt="Orion Belt: your laptop, the gateway and an agent on your server, drawn as the three stars of Orion's Belt. The agent connects out through a closed firewall; the gateway records the session." src="https://raw.githubusercontent.com/orion-belt-dev/.github/main/profile/assets/hero-light.svg" width="100%">
</picture>

Orion Belt is an open-source SSH access gateway you run yourself. An agent on each server connects **out** to the gateway, so your servers keep every inbound port closed. Everyone reaches them through the gateway, which checks who may log in, can ask a teammate for approval, and records the session.

**[Try it in 10 minutes](https://orion-belt.dev/docs/quickstart/try-in-10-minutes)** &nbsp;|&nbsp; [Documentation](https://orion-belt.dev/docs/introduction) &nbsp;|&nbsp; [Discord](https://discord.gg/w62S8jxTHJ) &nbsp;|&nbsp; [Star on GitHub](https://github.com/orion-belt-dev/orion-belt)

[![Latest release](https://img.shields.io/github/v/release/orion-belt-dev/orion-belt?style=flat-square&label=release&color=146ef5)](https://github.com/orion-belt-dev/orion-belt/releases/latest) [![GitHub stars](https://img.shields.io/github/stars/orion-belt-dev/orion-belt?style=flat-square&color=146ef5)](https://github.com/orion-belt-dev/orion-belt) [![Discord](https://img.shields.io/badge/discord-join_the_server-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/w62S8jxTHJ)

## Is it for you?

**A good fit** if you run Linux servers, want recorded and approved SSH access, and would rather not adopt a large zero-trust platform or open SSH to the internet on every host.

**Not yet** if you need OIDC single sign-on, RDP, Kubernetes or database proxying today. Those are on the [roadmap](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/ROADMAP.md), and early operators decide what comes first.

| | Orion Belt | Large access platforms | Plain bastion host |
| --- | --- | --- | --- |
| Inbound ports on your servers | None, agents connect out | Usually none | Open to the bastion |
| Session recording and live watch | Built in | Built in | Up to you |
| Just-in-time access with approval | Built in, also from Slack, Discord, Teams | Built in | Rare |
| What you operate | One gateway and PostgreSQL | A platform | A jump host |

## Run it

You need Docker. The script generates its own secrets, starts a gateway, connects a demo machine and prints a sign-in link.

```bash
git clone https://github.com/orion-belt-dev/orion-belt.git
cd orion-belt
./scripts/docker-quickstart.sh
```

1. Open **Machines**, choose **lab-1** and run a few commands in the web terminal.
2. Open **Sessions** and play back what you just did.
3. From your own terminal: `./bin/osh -c client.yaml root@lab-1`. Plain OpenSSH works through the gateway too.

For a real server, install the gateway with deb, rpm or apk packages or a one-line installer: [server setup](https://orion-belt.dev/docs/quickstart/server).

<img src="https://raw.githubusercontent.com/orion-belt-dev/orion-belt/master/assets/orion-belt-in-action.gif" alt="The Orion Belt console: opening a web terminal on a machine, then replaying the recorded session." width="100%">

## What ships today

- **Agents that connect out** over reverse SSH, packaged for deb, rpm and apk.
- **Session recording** with playback, live watch and optional encryption at rest.
- **Just-in-time access**: request, approve, and the grant expires on its own. Approve from the console, the API, or Slack, Discord, Teams and Rocket.Chat.
- **MFA** with TOTP and WebAuthn, and FIDO `sk-*` SSH keys.
- **Per-machine permissions** down to the remote user, with optional OpenFGA.
- **Optional SSH certificate authority** for short-lived certificates instead of long-lived keys.
- **Operations**: Prometheus metrics, OpenTelemetry traces, audit reports as PDF or CSV, an OpenAPI spec, and SDKs for Go, Python, JavaScript and .NET.

## Repositories

| Repository | What's in it |
| --- | --- |
| [orion-belt](https://github.com/orion-belt-dev/orion-belt) | Gateway, agent, `osh`, `ocp` and `oadmin` clients, web console, plugins and SDKs |
| [packages](https://github.com/orion-belt-dev/packages) | Signed package mirror used by the agent install scripts |
| [.github](https://github.com/orion-belt-dev/.github) | This profile and shared community files |

## Get involved

We're looking for **early operators**: people running Orion Belt in a lab or a small team who will tell us what broke and what's missing. Your setup notes shape the roadmap.

- **Running it?** Tell us how it went in [Discussions](https://github.com/orion-belt-dev/orion-belt/discussions) or on [Discord](https://discord.gg/w62S8jxTHJ).
- **Want to write code?** Start with a [good first issue](https://github.com/orion-belt-dev/orion-belt/issues?q=is%3Aopen+label%3A%22good+first+issue%22%2C%22good-first-issue%22) or a [small task](https://github.com/orion-belt-dev/orion-belt/issues?q=is%3Aopen+label%3Asize%3AS), then read the [contributing guide](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/CONTRIBUTING.md).
- **Know the area?** Open work is grouped by label: [protocols](https://github.com/orion-belt-dev/orion-belt/issues?q=is%3Aopen+label%3Aprotocols), [policy](https://github.com/orion-belt-dev/orion-belt/issues?q=is%3Aopen+label%3Apolicy), [compliance](https://github.com/orion-belt-dev/orion-belt/issues?q=is%3Aopen+label%3Acompliance) and [plugins and SDKs](https://github.com/orion-belt-dev/orion-belt/issues?q=is%3Aopen+label%3Aplatform).
- **Found a security issue?** Please report it privately through [GitHub security advisories](https://github.com/orion-belt-dev/orion-belt/security/advisories/new), not in a public issue.

## License

Apache 2.0 with the Commons Clause. You can self-host and use Orion Belt inside your company, including commercially, and change it as you like. You can't sell Orion Belt itself, or a hosted service built mainly on it. [Read the license](https://github.com/orion-belt-dev/orion-belt/blob/master/LICENSE).

<sub>Security infrastructure should be self-hosted, auditable, and boring to operate. &nbsp;[orion-belt.dev](https://orion-belt.dev)</sub>
