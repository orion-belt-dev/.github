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

## Get started

### Try it on your laptop

You need Docker: Docker Desktop on macOS and Windows, or Docker Engine with the Compose plugin on Linux. The script generates its own secrets, starts a gateway, connects a demo machine and prints a sign-in link.

```bash
git clone https://github.com/orion-belt-dev/orion-belt.git
cd orion-belt
./scripts/docker-quickstart.sh
```

1. Open **Machines**, choose **lab-1** and run a few commands in the web terminal.
2. Open **Sessions** and play back what you just did.
3. From your own terminal: `./bin/osh -c client.yaml root@lab-1`

Stop it with `./scripts/docker-quickstart.sh --down`.

<img src="https://raw.githubusercontent.com/orion-belt-dev/orion-belt/master/assets/orion-belt-in-action.gif" alt="The Orion Belt console: opening a web terminal on a machine, then replaying the recorded session." width="100%">

### Install on a server

The quickest way is the installer. It picks the right package for your distribution, can install PostgreSQL for you, writes `/etc/orion-belt/server.yaml`, starts the service and creates the first admin.

```bash
curl -fsSL https://raw.githubusercontent.com/orion-belt-dev/orion-belt/master/scripts/install-server.sh | sudo bash
```

To install the packages yourself, pick your system below. Every release has packages for amd64 and arm64. There is no APT or DNF repository yet, so you download the package and install the file.

<details>
<summary><b>Debian and Ubuntu</b> (apt)</summary>

```bash
VER=$(curl -fsSL https://orion-belt-dev.github.io/packages/VERSION)
ARCH=$(dpkg --print-architecture)
curl -fLO "https://github.com/orion-belt-dev/orion-belt/releases/download/v$VER/orion-belt_${VER}_linux_${ARCH}.deb"
sudo apt install "./orion-belt_${VER}_linux_${ARCH}.deb"
```
</details>

<details>
<summary><b>RHEL, Rocky, AlmaLinux and Fedora</b> (dnf)</summary>

```bash
VER=$(curl -fsSL https://orion-belt-dev.github.io/packages/VERSION)
ARCH=$(uname -m | sed 's/x86_64/amd64/; s/aarch64/arm64/')
curl -fLO "https://github.com/orion-belt-dev/orion-belt/releases/download/v$VER/orion-belt_${VER}_linux_${ARCH}.rpm"
sudo dnf install "./orion-belt_${VER}_linux_${ARCH}.rpm"
```

On openSUSE, install the same file with `sudo zypper install ./orion-belt_${VER}_linux_${ARCH}.rpm`.
</details>

<details>
<summary><b>Alpine</b> (apk, OpenRC)</summary>

```bash
VER=$(curl -fsSL https://orion-belt-dev.github.io/packages/VERSION)
ARCH=$(uname -m | sed 's/x86_64/amd64/; s/aarch64/arm64/')
curl -fLO "https://github.com/orion-belt-dev/orion-belt/releases/download/v$VER/orion-belt_${VER}_linux_${ARCH}.apk"
sudo apk add --allow-untrusted "./orion-belt_${VER}_linux_${ARCH}.apk"
```

`--allow-untrusted` is needed because the package is a local file, not from a signed index. Check its signature first (see below). Start it with `sudo rc-update add orion-belt-server && sudo rc-service orion-belt-server start`.
</details>

<details>
<summary><b>Arch Linux</b> (PKGBUILD)</summary>

```bash
git clone https://github.com/orion-belt-dev/orion-belt.git
cd orion-belt/packaging/arch
makepkg -si   # set pkgver to the release you want first
```
</details>

<details>
<summary><b>Check the signature</b> (any Linux)</summary>

Releases are signed by `Orion Belt Packaging <maintainers@orion-belt.dev>`.

```bash
B="https://github.com/orion-belt-dev/orion-belt/releases/download/v$VER"
curl -fLO "$B/checksums.txt" -fLO "$B/checksums.txt.sig"
curl -fsSL https://raw.githubusercontent.com/orion-belt-dev/orion-belt/master/packaging/keys/orion-belt.asc | gpg --import
gpg --verify checksums.txt.sig checksums.txt
sha256sum --ignore-missing -c checksums.txt
```
</details>

Then configure and start the gateway (systemd):

```bash
sudoedit /etc/orion-belt/server.yaml        # database URL, JWT secret, server.public_url
sudo systemctl enable --now orion-belt-server
sudo -u orionbelt orion-belt-server -c /etc/orion-belt/server.yaml setup   # creates the first admin
```

**Add your servers.** In the console, open **Add agent** and choose **Generate install script**. Run the script on the server: it installs `orion-belt-agent`, writes its config and starts it. The agent connects out to the gateway on port 2222, so the server needs no inbound rule. To do it by hand, see [Add agents](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/SETUP.md#3-add-agents).

### Install the clients

You don't need them: any OpenSSH client works, including the one built into Windows 10 and 11. `osh`, `ocp` and `oadmin` add sign-in, file copy, access requests and admin commands.

<details>
<summary><b>Linux</b></summary>

Same steps as the server packages above, with the `orion-belt-tools` package:

```bash
curl -fLO "https://github.com/orion-belt-dev/orion-belt/releases/download/v$VER/orion-belt-tools_${VER}_linux_${ARCH}.deb"
sudo apt install "./orion-belt-tools_${VER}_linux_${ARCH}.deb"   # or the .rpm / .apk file
```
</details>

<details>
<summary><b>macOS</b> (Apple silicon and Intel)</summary>

```bash
VER=$(curl -fsSL https://orion-belt-dev.github.io/packages/VERSION)
ARCH=$(uname -m | sed 's/x86_64/amd64/')
curl -fL "https://github.com/orion-belt-dev/orion-belt/releases/download/v$VER/orion-belt_tools_${VER}_darwin_${ARCH}.tar.gz" | tar xz osh ocp oadmin
sudo mv osh ocp oadmin /usr/local/bin/
```
</details>

### Everyday examples

The gateway listens for SSH on port 2222. These examples use `orion.example.com` as the gateway and `web-01` as a server.

```bash
# Open a shell on web-01 with plain OpenSSH, as gateway user alice
ssh -p 2222 alice+web-01@orion.example.com

# Run one command on web-01 as the remote user bob
ssh -p 2222 'alice+bob%web-01@orion.example.com' uptime

# Sign in once with osh; it reads the gateway from ~/.orion-belt/client.yaml
osh login
osh web-01

# Copy a file to and from web-01
ocp ./app.conf web-01:/etc/app/app.conf
ocp web-01:/var/log/app.log ./

# No access to db-01? Ask for one hour, with a reason
osh --request-access db-01 --reason "Rotate the TLS certificate" --duration 3600

# Operators: review and approve requests (also possible from the console or chat)
oadmin requests list
oadmin requests approve <request-id>

# Give alice standing access to web-01
oadmin permissions grant --user alice --machine web-01
```

More in the [client CLI reference](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/CLIENT-CLI.md) and [OpenSSH guide](https://github.com/orion-belt-dev/orion-belt/blob/master/docs/openssh-clients.md).

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
