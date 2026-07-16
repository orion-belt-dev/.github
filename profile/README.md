<!--
  Orion Belt — GitHub organization profile
  Repo: orion-belt-dev/.github
  Path: profile/README.md  →  shown on https://github.com/orion-belt-dev
-->

<div align="center">

<img src="https://raw.githubusercontent.com/orion-belt-dev/orion-belt/master/assets/banner-2.png" alt="Orion Belt" width="920" />

# Orion Belt

**Self-hosted SSH access gateway with PAM workflows**

Teleport-like SSH access control — without opening inbound ports or adopting a large platform.

[Website](https://orion-belt.dev) · [Documentation](https://orion-belt.dev/docs/introduction) · [Discord](https://discord.gg/w62S8jxTHJ) · [Try in 10 minutes](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/TRY_IN_10_MINUTES.md)

</div>

---

## What we build

**[orion-belt](https://github.com/orion-belt-dev/orion-belt)** — an open-source SSH/SCP bastion and privileged-access gateway for Linux-first teams.

| | |
| --- | --- |
| **Agents dial out** | Reverse SSH tunnels — no inbound firewall holes on targets |
| **Session recording** | Full audit trail + live watch |
| **JIT access** | Request / approve / expire (UI, API, ChatOps) |
| **MFA** | TOTP + WebAuthn; FIDO SSH keys |
| **Authorization** | ReBAC (+ optional OpenFGA) |
| **Optional SSH CA** | Short-lived certificates instead of standing keys |

<div align="center">
<img src="https://raw.githubusercontent.com/orion-belt-dev/orion-belt/master/assets/orion-belt-in-action.gif" alt="Orion Belt in action" width="920" />
</div>

---

## Start here

```bash
git clone https://github.com/orion-belt-dev/orion-belt.git
cd orion-belt
./scripts/docker-quickstart.sh
```

Then: add an agent → SSH through the gateway → open **Sessions** for playback.

Full walkthrough: **[Try Orion Belt in 10 minutes](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/TRY_IN_10_MINUTES.md)**

---

## Repositories

| Repo | Description |
| --- | --- |
| **[orion-belt](https://github.com/orion-belt-dev/orion-belt)** | Core gateway, agent, clients, and web console (v1.0) |
| **[.github](https://github.com/orion-belt-dev/.github)** | Organization profile & community health files |

---

## Community

We're looking for **early operators** — labs and small teams running v1.0 and giving sharp feedback.

- [Discord](https://discord.gg/w62S8jxTHJ)
- [GitHub Discussions](https://github.com/orion-belt-dev/orion-belt/discussions)
- [Issues](https://github.com/orion-belt-dev/orion-belt/issues)

---

## License

Orion Belt is **Apache 2.0 + Commons Clause**: free to self-host and use internally (including commercially). You cannot sell Orion Belt as a product or hosted service.

Details: [LICENSE](https://github.com/orion-belt-dev/orion-belt/blob/master/LICENSE) · [orion-belt.dev](https://orion-belt.dev)

---

<div align="center">

**Security infrastructure should be self-hosted, auditable, and boring to operate.**

[orion-belt.dev](https://orion-belt.dev) · [github.com/orion-belt-dev/orion-belt](https://github.com/orion-belt-dev/orion-belt)

</div>
