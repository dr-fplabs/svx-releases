# SVX downloads

Official release downloads for **SVX (Standard Virtual X)**, a self-service
portal for F5 BIG-IP. Application teams request standard virtual servers;
network administrators review, approve and push them. This repository holds
release files only; the source code is not published here.

## Download

Pick the bundle that suits your host:

- **[Docker bundle](https://github.com/dr-fplabs/svx-releases/releases/latest/download/svx-docker.tar.gz)**
  (`svx-docker.tar.gz`). Recommended. Needs Linux with Docker and Docker Compose.
- **[Native bundle](https://github.com/dr-fplabs/svx-releases/releases/latest/download/svx-native.tar.gz)**
  (`svx-native.tar.gz`). For hosts that can't run containers, such as
  unprivileged LXCs. Needs Linux x86_64 with Python 3.12.

Older versions are under [Releases](https://github.com/dr-fplabs/svx-releases/releases).
Each release lists a SHA-256 checksum for every file:

```bash
sha256sum -c SHA256SUMS --ignore-missing
```

## Install

Copy the bundle to the server, then:

```bash
tar xzf svx-docker.tar.gz        # or svx-native.tar.gz
cd svx-*/          # svx-<version>/ or svx-<version>-native/
./install.sh
```

The installer asks for your BIG-IP management address and service account,
creates the first admin account, and generates a TLS certificate. SVX then
runs on `https://<your-server>` (port 443) with Docker, or
`https://<your-server>:5000` natively — `./install.sh --port=N` picks another. The certificate is self-signed at
first, so expect a browser warning; put your own certificate in `certs/` to
replace it. Each bundle has a `README.md` to start from and an `INSTALL.md` with the
full guide.

The bundle is self-contained: the server needs no internet access, git,
PyPI or Docker Hub.

## Upgrade

Download the new bundle and run this from your existing install folder:

```bash
./upgrade.sh --bundle /path/to/svx-docker.tar.gz
```

It verifies the bundle, snapshots your data, keeps a rollback image, and
confirms the new version started. `./upgrade.sh --rollback` reverts.

## Licensing

SVX is **free for one F5 device and up to ten virtual servers** — no key or
sign-up needed, every feature included. Beyond that you need a licence key:

| Edition | Devices | Virtual servers | Term | Price |
|---|---|---|---|---|
| Free (no key) | 1 | 10 | No time limit | Free |
| Trial | Unlimited | Unlimited | 30 days | Free |
| 1-year | Unlimited | Unlimited | 1 year | £120 |
| 5-year | Unlimited | Unlimited | 5 years | £500 |

Prices are per portal installation. Major upgrades and new features may be
charged separately.

Keys come from DDR Computing Ltd at info@ddrcomputing.co.uk. Copy the key to
`config/license.key`; it is checked offline on your server. When a key expires
SVX carries on as the Free edition — nothing is locked out.

F5 and BIG-IP are trademarks of F5, Inc. SVX is not affiliated with or
endorsed by F5, Inc.

© DDR Computing Ltd. All rights reserved.
