<h1 align="center">
  <img src="https://github.com/user-attachments/assets/9400b5d0-0c96-427c-a438-c81f526e8f95" width="400">
</h1><br>


This repository provides a **starter template** for creating your own personal configuration repository for use with [fire-flake](https://github.com/adhityaravi/fire-flake).

---

## Purpose

- Store **personal variables** (e.g., names, preferences, system configurations) in the `vars/` folder.
- Manage **private secrets** (e.g., API keys, passwords, tokens) in the `secrets/` folder.
- Allow each user to create a **private fire-flake-config repo**, without modifying the main fire-flake codebase.
- Enable clean separation between public and private data.
- Make it easy to update, manage, and sync your configuration as fire-flake evolves.

## Structure

```bash
fire-flake-config/
├── flake.nix       # Defines the configuration flake
├── vars/           # Personal, non-sensitive configuration files (as Nix files)
├── secrets/        # Private, sensitive configuration files
└── .gitignore      # Ensures secrets and build artifacts are not committed
```

> **Important:** The folder structure inside `vars/` and `secrets/` **must mirror** the `fire-flake` folder structure in the [fire-flake](https://github.com/adhityaravi/fire-flake/tree/main/fire-flake) repository. This is essential for consistency, interoperability, and proper functioning.

### flake.nix

This file defines the configuration outputs:

```nix
{
  description = "Personal configuration files for fire-flake";

  outputs = { self, ... }: {
    fireFlakeConfig = {
      paths = {
        vars = ./vars;
        secrets = ./secrets;
      };

      meta = {
        owner = "adhityaravi";
        version = "0.0.1-beta";
      };
    };
  };
}
```

You are encouraged to customize the `owner` and `version` fields for your own repo.

## How to Use

1. **Create a new private repository** by using this repo as a template (GitHub allows "Use this template").
2. Modify/add files under `vars/` to define your personal data.
3. Modify/add files under `secrets/` carefully (recommended to encrypt or manage safely).
4. Ensure your folder structure inside `vars/` and `secrets/` matches the `fire-flake` repo.
5. Update `flake.nix` if needed (e.g., change `owner` or paths).
6. Point your [fire-flake](https://github.com/adhityaravi/fire-flake) configuration to use your private `fire-flake-config` as an input flake.

Example snippet in your `fire-flake` repo:

```nix
inputs.fire-flake-config.url = "github:<your-username>/<your-private-fire-flake-config>";
```