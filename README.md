# renovate-config

This repository contains some common sense configuration for Renovate. These configuration CAN be used to extend the local repository configuration in the renovate.json in other repositories. Renovate documentation refer to this method as [Shareable Config Presets](https://docs.renovatebot.com/config-presets).

## How It Works

We use a three-tiered system for renovate configuration. The goal is to provide flexibility for developers, while giving them the option to easily follow best practices.

- **Central Configuration:** Our central configuration, which is directly applied on our renovate-bot, only contains operational configuration. This configuration is managed in our private [renovate-bot repository](https://github.com/wigo4it/renovate-bot/blob/main/.github/renovate-config.json).
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
