---
title: Home
---

[<img src="https://simpleicons.org/icons/github.svg" style="max-width:15%;min-width:40px;float:right;" alt="Github repo" />](https://github.com/servicer-labs/servicer)

# 🔧 servicer

[![Crates.io](https://img.shields.io/crates/v/servicer?style=flat-square)](https://crates.io/crates/servicer)
[![Crates.io](https://img.shields.io/crates/d/servicer?style=flat-square)](https://crates.io/crates/servicer)
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE-MIT)

## Simplify Service Management on systemd

`servicer` is a user-friendly CLI tool designed to simplify service management on `systemd`, abstracting away the complexities of the systemd ecosystem. With an easy-to-use API comparable to popular tools like `pm2`, servicer empowers users to create, control, and manage services effortlessly.

`servicer` is lightweight, written in Rust and doesn't run in the background. It does not fork services nor run a custom logging solution. It is a thin layer on `systemd` that creates `.ser.service` files. Logging is handled by journald.

###  Install

Download the binary from the [release page](https://github.com/servicer-labs/servicer/releases/download/v0.1.2/servicer) or setup as-

```
wget https://github.com/servicer-labs/servicer/releases/download/v0.1.2/servicer

# grant permissions
chmod +rwx ./servicer

# Rename to ser and make it accessable from path
sudo mv ./servicer /usr/bin/ser

# This should work now
ser --help
```

Or build from source

```
cargo install servicer
sudo ln -s ~/.cargo/bin/servicer /usr/bin/ser
```

### Create service

```
sudo ser create index.js --start --enable
```

Or write your own custom `.service` file. `servicer` provides a starter template to get you started quickly.

```
sudo ser edit index.js
```

Got an existing service? No problem. Rename your `.service` file to `.ser.service` and servicer will pick it up.

### View services

```
ser status
```

```
+-------+-------------+--------+----------------+-------+--------+
| pid   | name        | active | enable on boot | cpu % | memory |
+-------+-------------+--------+----------------+-------+--------+
| 24294 |    index.js | active | true           | 0     | 9.5 KB |
+-------+-------------+--------+----------------+-------+--------+
```

### View logs

```
ser logs index.js
```

### Stop, disable or delete

```
# Stop a running service
sudo ser stop index.js

# Disable load on boot
sudo ser disable index.js

# Delete the .service file
sudo ser rm index.js
```

### View file and unit path

```
ser which index.js
```

```
Paths for index.js.ser.service:
+--------------+-----------------------------------------------------------+
| name         | path                                                      |
+--------------+-----------------------------------------------------------+
| Service file | /etc/systemd/system/index.js.ser.service                  |
+--------------+-----------------------------------------------------------+
| Unit file    | /org/freedesktop/systemd1/unit/index_2ejs_2eser_2eservice |
+--------------+-----------------------------------------------------------+
```
