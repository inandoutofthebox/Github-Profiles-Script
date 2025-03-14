# Git Profile Manager for WSL2

#

<div align=center>
<img src="https://raw.githubusercontent.com/inandoutofthebox/Github-Profiles-Script/refs/heads/main/Logo.jpg">
</div>

#

The Git Profile Manager is a powerful tool that helps you manage multiple Git identities (name, email, GitHub username, SSH keys) and automatically switches between those Github-Accounts based on your current working directory. This is especially useful for developers who work on different projects requiring different Git credentials. This can get quiete an hussle to change back and forth and be breaking Productivity in some cases. This Script easily helps with it. Just configure it once and benefit longterm from it. 

#

What inspired this project? Simply put, I identified a genuine need that wasn't being addressed by existing solutions. When I couldn't find anything that matched my requirements expect an Youtube Video that does it all manual, I decided to create an more Automated solution myself.

#

Fun fact: This project was also created with the help of this script, which demonstrates the practical applicability and effectiveness of the Git Profile Manager in real development environments.

#

Execute for install 

```bash

curl -sL https://raw.githubusercontent.com/inandoutofthebox/Github-Profiles-Script/main/git-profile -o git-profile && chmod +x git-profile && ./git-profile install

```

Use it with just writing: 
```bash
git-profile
```

## Features

- **Multiple Profiles**: Manage different Git identities for work, personal, and other projects
- **SSH Key Management**: Easy integration and management of SSH keys for each profile
- **Automatic Profile Switching**: Changes your Git configuration automatically when you switch directories
- **WSL2 Optimized**: Specifically designed for Windows Subsystem (Tested with Ubunt 24.04 LTS) for Linux 2 environments

## Commands

Here are the main commands available in the Git Profile Manager:

```bash

git-profile
Git Profile Manager for WSL2

Usage:
    git-profile create <name> <email> <github-user> [directory]  - Creates a new profile
    git-profile add-dir <name> <directory>                       - Adds a directory to a profile
    git-profile switch <name>                                    - Switches to a profile
    git-profile auto                                             - Automatically switches based on the current directory
    git-profile auto debug                                       - Shows debug information during profile switching
    git-profile list                                             - Lists all profiles
    git-profile install                                          - Installs the script to /usr/local/bin and sets up .bashrc
    git-profile help                                             - Shows this help

Examples:
    git-profile create "Work" "max@company.com" "MaxCompany" "/path/to/projects/work/"
    git-profile add-dir "Work" "/path/to/additional/work/projects/"
    git-profile install

```

## Usage Examples

### Creating a Profile

To create a new profile for work projects:

```bash
git-profile create "Work" "your.email@company.com" "YourGitHubUser" "/path/to/work/projects"
```

This command will:
1. Ask if you want to create or use an existing SSH key
2. Create a profile named "Work" with your work email and GitHub username
3. Associate the specified directory with this profile

### Adding Directories to a Profile

To add another directory to an existing profile:

```bash
git-profile add-dir "Work" "/path/to/another/work/project"
```

### Switching Profiles Manually

To manually switch to a specific profile:

```bash
git-profile switch "Personal"
```

### Automatic Profile Switching

The tool automatically switches your Git profile when you change directories. Simply:

```bash
cd /path/to/work/projects
# Your Git configuration will automatically switch to the "Work" profile
```

### Listing All Profiles

To see all your configured profiles:

```bash
git-profile list
```

## How It Works

The Git Profile Manager stores all profiles in a JSON file at `~/.git_profiles.json`. When you change directories, it checks if the current directory is associated with a known profile and automatically switches to that profile.

When switching profiles, the tool sets these Git configurations:
- `user.name`
- `user.email`
- `github.user` 
- `core.sshCommand` (if an SSH key is configured)

## SSH Key Management

The tool helps you manage SSH keys for different accounts:

1. You can create a new SSH key for each profile
2. You can use existing SSH keys for profiles
3. The tool automatically configures Git to use the correct SSH key for each profile

## Troubleshooting

If automatic profile switching isn't working, ensure:
1. The current directory is a Git repository (`git init` or cloned)
2. The directory is properly associated with a profile
3. You have the appropriate configuration in your `.bashrc` file

For more detailed debugging information, use:
```bash
git-profile auto debug
```

This comprehensive tool makes working with multiple Git accounts seamless and eliminates the hassle of manually changing your Git configuration when switching between projects.
