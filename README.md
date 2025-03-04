# MinIO Quickstart Guide
[![Slack](https://slack.min.io/slack?type=svg)](https://slack.min.io) [![Docker Pulls](https://img.shields.io/docker/pulls/minio/minio.svg?maxAge=604800)](https://hub.docker.com/r/minio/minio/) [![license](https://img.shields.io/badge/license-AGPL%20V3-blue)](https://github.com/minio/minio/blob/master/LICENSE)

[![MinIO](https://raw.githubusercontent.com/minio/minio/master/.github/logo.svg?sanitize=true)](https://min.io)

MinIO is a High Performance Object Storage released under GNU Affero General Public License v3.0. It is API compatible with Amazon S3 cloud storage service. Use MinIO to build high performance infrastructure for machine learning, analytics and application data workloads.

This README provides quickstart instructions on running MinIO on baremetal hardware, including container-based installations. For Kubernetes environments, use the [MinIO Kubernetes Operator](https://github.com/minio/operator/blob/master/README.md).

# Container Installation

Use the following commands to run a standalone MinIO server as a container.

Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication
require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically,
with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html)
for more complete documentation.

## Stable

Run the following command to run the latest stable image of MinIO as a container using an ephemeral data volume:

```sh
podman run -p 9000:9000 -p 9001:9001 \
  quay.io/minio/minio server /data --console-address ":9001"
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Console, an embedded
object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the
root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See
[Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers,
see https://docs.min.io/docs/ and click **MinIO SDKs** in the navigation to view MinIO SDKs for supported languages.

> NOTE: To deploy MinIO on with persistent storage, you must map local persistent directories from the host OS to the container using the `podman -v` option. For example, `-v /mnt/data:/data` maps the host OS drive at `/mnt/data` to `/data` on the container.

# macOS

Use the following commands to run a standalone MinIO server on macOS.

Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically, with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html) for more complete documentation.

## Homebrew (recommended)

Run the following command to install the latest stable MinIO package using [Homebrew](https://brew.sh/). Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

```sh
brew install minio/stable/minio
minio server /data
```

> NOTE: If you previously installed minio using `brew install minio` then it is recommended that you reinstall minio from `minio/stable/minio` official repo instead.

```sh
brew uninstall minio
brew install minio/stable/minio
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Console, an embedded web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See [Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers, see https://docs.min.io/docs/ and click **MinIO SDKs** in the navigation to view MinIO SDKs for supported languages.

## Binary Download

Use the following command to download and run a standalone MinIO server on macOS. Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

```sh
wget https://dl.min.io/server/minio/release/darwin-amd64/minio
chmod +x minio
./minio server /data
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Console, an embedded web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See [Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers, see https://docs.min.io/docs/ and click **MinIO SDKs** in the navigation to view MinIO SDKs for supported languages.

# GNU/Linux

Use the following command to run a standalone MinIO server on Linux hosts running 64-bit Intel/AMD architectures. Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

```sh
wget https://dl.min.io/server/minio/release/linux-amd64/minio
chmod +x minio
./minio server /data
```

Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

The following table lists supported architectures. Replace the `wget` URL with the architecture for your Linux host.

| Architecture                   | URL                                                        |
| --------                       | ------                                                     |
| 64-bit Intel/AMD               | https://dl.min.io/server/minio/release/linux-amd64/minio   |
| 64-bit ARM                     | https://dl.min.io/server/minio/release/linux-arm64/minio   |
| 64-bit PowerPC LE (ppc64le)    | https://dl.min.io/server/minio/release/linux-ppc64le/minio |
| IBM Z-Series (S390X)           | https://dl.min.io/server/minio/release/linux-s390x/minio   |

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Console, an embedded web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See [Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers, see https://docs.min.io/docs/ and click **MinIO SDKs** in the navigation to view MinIO SDKs for supported languages.

> NOTE: Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically, with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html) for more complete documentation.

# Microsoft Windows

To run MinIO on 64-bit Windows hosts, download the MinIO executable from the following URL:

```sh
https://dl.min.io/server/minio/release/windows-amd64/minio.exe
```

Use the following command to run a standalone MinIO server on the Windows host. Replace ``D:\`` with the path to the drive or directory in which you want MinIO to store data. You must change the terminal or powershell directory to the location of the ``minio.exe`` executable, *or* add the path to that directory to the system ``$PATH``:

```sh
minio.exe server D:\
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Console, an embedded web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See [Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers, see https://docs.min.io/docs/ and click **MinIO SDKs** in the navigation to view MinIO SDKs for supported languages.

> NOTE: Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically, with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html) for more complete documentation.

# Install from Source

Use the following commands to compile and run a standalone MinIO server from source. Source installation is only intended for developers and advanced users. If you do not have a working Golang environment, please follow [How to install Golang](https://golang.org/doc/install). Minimum version required is [go1.17](https://golang.org/dl/#stable)

```sh
GO111MODULE=on go install github.com/minio/minio@latest
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Console, an embedded web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See [Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers, see https://docs.min.io/docs/ and click **MinIO SDKs** in the navigation to view MinIO SDKs for supported languages.

> NOTE: Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically, with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html) for more complete documentation.

MinIO strongly recommends *against* using compiled-from-source MinIO servers for production environments.

# Deployment Recommendations

## Allow port access for Firewalls

By default MinIO uses the port 9000 to listen for incoming connections. If your platform blocks the port by default, you may need to enable access to the port.

### ufw

For hosts with ufw enabled (Debian based distros), you can use `ufw` command to allow traffic to specific ports. Use below command to allow access to port 9000

```sh
ufw allow 9000
```

Below command enables all incoming traffic to ports ranging from 9000 to 9010.

```sh
ufw allow 9000:9010/tcp
```

### firewall-cmd

For hosts with firewall-cmd enabled (CentOS), you can use `firewall-cmd` command to allow traffic to specific ports. Use below commands to allow access to port 9000

```sh
firewall-cmd --get-active-zones
```

This command gets the active zone(s). Now, apply port rules to the relevant zones returned above. For example if the zone is `public`, use

```sh
firewall-cmd --zone=public --add-port=9000/tcp --permanent
```

Note that `permanent` makes sure the rules are persistent across firewall start, restart or reload. Finally reload the firewall for changes to take effect.

```sh
firewall-cmd --reload
```

### iptables

For hosts with iptables enabled (RHEL, CentOS, etc), you can use `iptables` command to enable all traffic coming to specific ports. Use below command to allow
access to port 9000

```sh
iptables -A INPUT -p tcp --dport 9000 -j ACCEPT
service iptables restart
```

Below command enables all incoming traffic to ports ranging from 9000 to 9010.

```sh
iptables -A INPUT -p tcp --dport 9000:9010 -j ACCEPT
service iptables restart
```

## Pre-existing data
When deployed on a single drive, MinIO server lets clients access any pre-existing data in the data directory. For example, if MinIO is started with the command  `minio server /mnt/data`, any pre-existing data in the `/mnt/data` directory would be accessible to the clients.

The above statement is also valid for all gateway backends.

# Test MinIO Connectivity

## Test using MinIO Console
MinIO Server comes with an embedded web based object browser. Point your web browser to http://127.0.0.1:9000 to ensure your server has started successfully.

> NOTE: MinIO runs console on random port by default if you wish choose a specific port use `--console-address` to pick a specific interface and port.

### Things to consider
MinIO redirects browser access requests to the configured server port (i.e. `127.0.0.1:9000`) to the configured Console port. MinIO uses the hostname or IP address specified in the request when building the redirect URL. The URL and port *must* be accessible by the client for the redirection to work.

For deployments behind a load balancer, proxy, or ingress rule where the MinIO host IP address or port is not public, use the `MINIO_BROWSER_REDIRECT_URL` environment variable to specify the external hostname for the redirect. The LB/Proxy must have rules for directing traffic to the Console port specifically.

For example, consider a MinIO deployment behind a proxy `https://minio.example.net`, `https://console.minio.example.net` with rules for forwarding traffic on port :9000 and :9001 to MinIO and the MinIO Console respectively on the internal network. Set `MINIO_BROWSER_REDIRECT_URL` to `https://console.minio.example.net` to ensure the browser receives a valid reachable URL.

Similarly, if your TLS certificates do not have the IP SAN for the MinIO server host, the MinIO Console may fail to validate the connection to the server. Use the `MINIO_SERVER_URL` environment variable  and specify the proxy-accessible hostname of the MinIO server to allow the Console to use the MinIO server API using the TLS certificate.

For example: `export MINIO_SERVER_URL="https://minio.example.net"`


| Dashboard                                                                                   | Creating a bucket                                                                           |
| -------------                                                                               | -------------                                                                               |
| ![Dashboard](https://github.com/minio/minio/blob/master/docs/screenshots/pic1.png?raw=true) | ![Dashboard](https://github.com/minio/minio/blob/master/docs/screenshots/pic2.png?raw=true) |

## Test using MinIO Client `mc`
`mc` provides a modern alternative to UNIX commands like ls, cat, cp, mirror, diff etc. It supports filesystems and Amazon S3 compatible cloud storage services. Follow the MinIO Client [Quickstart Guide](https://docs.min.io/docs/minio-client-quickstart-guide) for further instructions.

# Upgrading MinIO
MinIO server supports rolling upgrades, i.e. you can update one MinIO instance at a time in a distributed cluster. This allows upgrades with no downtime. Upgrades can be done manually by replacing the binary with the latest release and restarting all servers in a rolling fashion. However, we recommend all our users to use [`mc admin update`](https://docs.min.io/docs/minio-admin-complete-guide.html#update) from the client. This will update all the nodes in the cluster simultaneously and restart them, as shown in the following command from the MinIO client (mc):

```
mc admin update <minio alias, e.g., myminio>
```

> NOTE: some releases might not allow rolling upgrades, this is always called out in the release notes and it is generally advised to read release notes before upgrading. In such a situation `mc admin update` is the recommended upgrading mechanism to upgrade all servers at once.

## Important things to remember during MinIO upgrades

- Container environments are advised to update the container images instead of updating binaries inside the container.
- `mc admin update` is disabled in kubernetes/container environments, container environments provide their own mechanisms to rollout of updates.
- `mc admin update` will only work if the user running MinIO has write access to the parent directory where the binary is located, for example if the current binary is at `/usr/local/bin/minio`, you would need write access to `/usr/local/bin`.
- `mc admin update` updates and restarts all servers simultaneously, applications would retry and continue their respective operations upon upgrade.
- If using `kes` as KMS with MinIO, just replace the binary and restart `kes` more information about `kes` can be found [here](https://github.com/minio/kes/wiki)

# Explore Further
- [MinIO Erasure Code QuickStart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide)
- [Use `mc` with MinIO Server](https://docs.min.io/docs/minio-client-quickstart-guide)
- [Use `aws-cli` with MinIO Server](https://docs.min.io/docs/aws-cli-with-minio)
- [Use `s3cmd` with MinIO Server](https://docs.min.io/docs/s3cmd-with-minio)
- [Use `minio-go` SDK with MinIO Server](https://docs.min.io/docs/golang-client-quickstart-guide)
- [The MinIO documentation website](https://docs.min.io)

# Contribute to MinIO Project
Please follow MinIO [Contributor's Guide](https://github.com/minio/minio/blob/master/CONTRIBUTING.md)

# License
- MinIO source is licensed under the GNU AGPLv3 license that can be found in the [LICENSE](https://github.com/minio/minio/blob/master/LICENSE) file.
- MinIO [Documentation](https://github.com/minio/minio/tree/master/docs) © 2021 by MinIO, Inc is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- [License Compliance](https://github.com/minio/minio/blob/master/COMPLIANCE.md)
