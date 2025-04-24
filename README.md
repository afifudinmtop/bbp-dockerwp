
# Wordfence Docker WordPress Research Lab

**DockerWP** is a pre-configured Docker-based WordPress environment designed for vulnerability research, testing, and debugging. It is used by the [Wordfence Bug Bounty Program](https://www.wordfence.com/threat-intel/bug-bounty-program/) and provides researchers with a portable, flexible, and repeatable local lab setup.

---

## 📁 Folder Structure

This repository contains **two** lab environments for testing against different PHP versions:

- `dockerwp74/` – WordPress on **PHP 7.4**  
- `dockerwp84/` – WordPress on **PHP 8.4**

> NOTE: Exploitation of certain vulnerabilities, like PHAR deserialization, will only work on PHP 7.4
---

## 🧰 Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Windows / macOS / Linux)
- Git (to clone this repo)

---

## 🚀 Installation & Usage

1. **Clone this repository:**

   ```bash
   git clone https://github.com/wordfence/dockerwp-lab.git
   cd dockerwp-lab

2. **Choose a lab environment:**

    * For PHP 7.4:
    ```bash
    cd dockerwp74
    ```
    * For PHP 8.4:
    ```bash
    cd dockerwp84
    ```
3. **Build the environment:**

```bash
docker-compose build
```

4. **Start the environment:**

```bash
docker-compose up -d
```

5. Access WordPress

    * Visit http://localhost:1337 to complete the WordPress installation.

## 💻 Mac M1/M2 Compatibility

If you're running on an Apple Silicon Mac (M1/M2), Docker may fail to start containers due to architecture differences. You might see:

```bash
no matching manifest for linux/arm64/v8 in the manifest list entries
```

To resolve this:

1. Edit your `docker-compose.yml`
2. Add this line to **each service** mentioned in the file:

```yaml
platform: linux/amd64
```

3. If you're using MySQL, consider switching to:

```yaml
image: mariadb:latest
```

## ✉️ Mailcatcher Setup

Mailcatcher is included to help test email functionality like password resets or new user notifications.

* Mailcatcher UI: http://localhost:1080
* SMTP Host: `mailcatcher`
* SMTP Port: `1025`

### 🔧 WordPress SMTP Configuration

Use Simple SMTP for easy setup:

1. Install Simple SMTP from the WordPress plugin repository.
2. In plugin settings:
    * SMTP Host: `mailcatcher`
    * SMTP Port: `1025`
    * Use SMTP Authentication: `No`
3. Save settings and trigger a test email.

Emails will appear in the Mailcatcher UI at `http://localhost:1080`

## 🛠 Adminer

Adminer is a single-file MySQL database manager included in both configurations by default.

* Access it at: http://localhost:1337/adminer.php
* Login credentials match those defined in your docker-compose.yml

## 🐞 XDebug Support

Both environments come with XDebug pre-installed and configured.

### VSCode Setup

1. Install the [PHP Debug extension by Xdebug](https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug).
2. Open the “Run and Debug” panel in VSCode.
3. Click “create a launch.json” and select PHP.
4. VSCode will generate a working config — no need to manually edit it unless customizing path mappings.

## 🧪 WP-CLI Access

The `wpcli` container lets you use the full WP-CLI command line tool.

```bash
docker-compose exec wpcli wp plugin list
docker-compose exec wpcli wp user create test test@example.com --role=subscriber --user_pass=password
```

### Set Up an Alias for WP-CLI

To use WP-CLI as a one-liner from your terminal, add this to your shell profile:

* bash/zsh (`~/.bashrc` or `~/.zshrc`):

```bash
alias wp='docker-compose run --rm wpcli'
```

* Windows (Command Prompt):

```cmd
doskey wp=docker-compose.exe run --rm wpcli
```

Now you can run commands like:

```bash
wp plugin install wordfence --activate
```

## 📢 Have Questions or Need Help?

Join the Wordfence Researcher Discord:
👉 https://discord.com/invite/awPVjTNTrn

## 📚 More Info

Read the full setup and usage guide in the blog post:

👉 WordPress Security Research Series: Setting Up Your Research Lab