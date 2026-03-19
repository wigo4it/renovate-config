# renovate-config

This repository contains some common sense configuration for Renovate. These configuration CAN be used to extend the local repository configuration in the renovate.json in other repositories. Renovate documentation refer to this method as [Shareable Config Presets](https://docs.renovatebot.com/config-presets).

## How It Works

We use a three-tiered system for renovate configuration. The goal is to provide flexibility for developers, while giving them the option to easily follow best practices.

- **Global Configuration:** Our self-hosted renovate bot is managed in our private [renovate-bot repository](https://github.com/wigo4it/renovate-bot/blob/main/.github/renovate-config.json). This repository also contains a barebones global configuration (only for operational settings).
- **Shareable Preset Configurations:** The configuration files found in this repository. These include configs for multiple different types of packages, as well as a default config with some general best-practice settings.
- **Repository-Specific Settings**: Each target repository has its own custom configuration in ```renovate.json```. This is where the shareable preset configurations can be invoked (extended).


To use a shareable preset in a repository, you need to extend them in ```renovate.json``` in your repository. For example:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>wigo4it/renovate-config",
    "github>wigo4it/renovate-config:terraform",
    "github>wigo4it/renovate-config:helm"
  ]
}
```

In this example, the first extension uses ```default.json``` from this repository. The others refer to ```terraform.json``` and ```helm.json```.

## Why is this repository public?

We will use these renovate presets from both private and public repositories. [Renovate documentation](https://docs.renovatebot.com/getting-started/private-packages/#private-config-presets) says:

```markdown
It's not recommended that you use a private repository to host your config while then extending it from a public repository. If your preset doesn't have secrets then you should make it public, while if it does have secrets then it's better to split your preset between a public one which all repos extend, and a private one with secrets which only other private repos extend.
```
