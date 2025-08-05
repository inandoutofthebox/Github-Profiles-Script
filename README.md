<div align="center">
<img src="https://raw.githubusercontent.com/inandoutofthebox/Github-Profiles-Script/refs/heads/main/Logo.jpg">
</div>

**Git Profile Manager** is an advanced Bash script that lets you manage multiple Git identities (name, email, GitHub username, SSH key) safely and switch between them automatically or manually—based on the directory you are working in. It features interactive SSH key management, debugging, full backup/restore, seamless WSL2/Linux integration, and autoswitch via `.bashrc`.

---

## Why?

If you work with different GitHub accounts (business, private, open source), keeping your profiles in sync quickly becomes a hassle. Most tutorials are manual and error-prone. **Git Profile Manager** solves this elegantly and securely—install once, benefit forever.  
> This whole repository is managed with this tool, so it’s always field-tested.

---

## Installation

```

curl -sL https://raw.githubusercontent.com/inandoutofthebox/Github-Profiles-Script/main/git-profile -o git-profile
chmod +x git-profile
./git-profile install

```

The installation sets up the script in `/usr/local/bin/git-profile` and integrates in your `.bashrc` if you want auto profile switching.

---

## Features

- **Multiple Profiles:** Name, email, GitHub user, SSH key, directories, created timestamp per profile.
- **SSH Key Wizard:** Create a new SSH key (ED25519, RSA4096/2048) or select from existing, all in an interactive menu. Keys are automatically loaded into `ssh-agent`.
- **Auto or Manual Switching:** Automatically assigns the right profile (Git config + SSH key) as you `cd` into a project directory.
- **Interactive & Secure:** All console inputs are validated and color-coded. Clear success, warning, and error messages.
- **Profile Management:** List, view, backup, restore, delete, get status, and see config path at any time.
- **Logging:** All actions and debug output go to `~/.git_profile_manager.log`.
- **Advanced Bashrc Integration:** Optional, overwrites `cd` to call `git-profile auto` after every directory change.
- **WSL2 and Linux Native:** Tested on Ubuntu 24.04 under WSL2, but works in any Unix-like shell with Bash and `jq`.

---

## Usage

### Main Commands

```

git-profile create <name> <email> <github-user> [directory]   \# Create a profile and (optionally) assign a directory
git-profile add-dir <name> <directory>                        \# Link more directories to a profile
git-profile switch <name>                                     \# Switch manually to a profile
git-profile auto                                              \# Auto-switch profile based on your current directory
git-profile auto debug                                        \# Like above, but with detailed debug output
git-profile list                                              \# List all profiles with their information
git-profile delete <name>                                     \# Delete a profile (with confirmation)
git-profile status                                            \# View current status, active profile \& git config
git-profile config                                            \# Show script, log, and config locations
git-profile backup                                            \# Back up your current profiles configuration
git-profile restore [backupfile]                              \# Restore a backup
git-profile install                                           \# Install/repair setup (Bashrc, etc.)
git-profile version                                           \# Show script version
git-profile help                                              \# Command overview and usage

```

### Example Workflow

```

git-profile create "Business" "office@company.com" "AcmeDev" "~/projects/company"
git-profile add-dir "Business" "~/other/company-stuff"
git-profile create "Private" "jack@home.org" "jackhack" "~/code/private"
cd ~/projects/company          \# Auto-switches to Business profile!
git-profile list               \# See all saved profiles and their settings
git-profile status             \# Check which profile is currently active

```

---

## Bashrc Integration

When you run `git-profile install`, you’ll be offered to enable autoswitch:

- `cd` is wrapped so every directory change triggers `git-profile auto`
- On shell start you’ll get the right profile if you’re inside a mapped directory

To activate new changes:
```

source ~/.bashrc

```

---

## Data Storage & Example

All your config is stored in these files:
- **Profiles:** `~/.git_profiles.json`
- **Logs:**     `~/.git_profile_manager.log`
- **SSH Keys:** Saved wherever you want under `~/.ssh/`

Example `~/.git_profiles.json`:

```

{
"Business": {
"user.name": "Acme Dev",
"user.email": "office@company.com",
"github.user": "AcmeDev",
"ssh.key": "/home/youruser/.ssh/id_business_ed25519",
"directories": [
"/home/youruser/projects/company",
"/home/youruser/other/company-stuff"
],
"created": "2025-08-05 13:33:00"
},
"Private": {
"user.name": "Jack User",
"user.email": "jack@home.org",
"github.user": "jackhack",
"ssh.key": "/home/youruser/.ssh/id_private_rsa4096",
"directories": ["/home/youruser/code/private"],
"created": "2025-08-05 13:35:12"
}
}

```

---

## SSH Key Management

- **Create:** Generates new keys per profile (ED25519/RSA, freely selectable).
- **Reuse:** Select from any existing keys in `~/.ssh/` interactively.
- **Agent:** Keys are added to running `ssh-agent` automatically (if available).
- **Clipboard:** Public key copied to clipboard on creation (if `xclip` or `pbcopy` is installed).

---

## Troubleshooting

- The current directory must be a Git repo (`git init` or clone)
- Make sure you assigned the directory to a profile
- Install `jq` with `apt install jq` if missing
- If autoswitch doesn’t work, check your `.bashrc` and rerun `git-profile install`
- To debug:
    ```
    git-profile auto debug
    ```

---

## Contribution

Open source & PRs/feedback warmly welcome!

---

## License

MIT License

---
