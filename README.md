# Renovate Presets Collection

A collection of custom [Renovate](https://docs.renovatebot.com/) preset configurations for handling various dependencies with proper versioning.

## Overview

This repository contains multiple preset configurations for Renovate bot to correctly parse and update dependencies in your projects. Each preset provides custom versioning rules for specific package ecosystems and repositories.

## Installation

To use all presets in your project, add the following to your Renovate configuration:

```json
{
  "extends": ["github>onelitefeathernet/renovate"]
}
```

To use a specific preset, reference it directly:

```json
{
  "extends": ["github>onelitefeathernet/renovate:paper"]
}
```

## Features

- Custom versioning rules for various package ecosystems
- Proper handling of specific versioning schemes
- Seamless integration with Renovate's dependency update system
- Modular design allowing you to use only the presets you need

## Available Presets

### Paper Preset

The Paper preset provides custom versioning for Paper API dependencies used in Minecraft server projects.

**Configuration:**

```json
{
  "packageRules": [
    {
      "matchDatasources": ["maven"],
      "matchPackageNames": ["io.papermc.paper:paper-api"],
      "versioning": "regex:^(?<major>\\d+)\\.(?<minor>\\d+)\\.(?<patch>\\d+)-.*$"
    }
  ]
}
```

This configuration ensures that Paper API dependencies are correctly versioned according to their semantic versioning pattern.

**Usage:**

```json
{
  "extends": ["github>onelitefeathernet/renovate:paper"]
}
```

### Minestom Preset

The Minestom preset provides custom versioning for Minestom dependencies used in Minecraft server projects.

**Configuration:**

```json
{
  "packageRules": [
    {
      "matchPackageNames": ["net.minestom:minestom"],
      "versioning": "regex:^(?<major>\\d{4})\\.(?<minor>\\d{2})\\.(?<patch>\\d{2})(?<prerelease>[a-zA-Z]?)-(?<build>[A-Za-z0-9._]+)$"
    }
  ]
}
```

This configuration ensures that Minestom dependencies are correctly versioned according to their date-based versioning pattern (YYYY.MM.DD format).

**Usage:**

```json
{
  "extends": ["github>onelitefeathernet/renovate:minestom"]
}
```

### Default Preset

The Default preset provides a general-purpose configuration for Renovate with common settings and best practices.

**Configuration:**

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "config:recommended",
    ":automergePatch",
    ":assignee({{arg0}})",
    ":timezone(Europe/Berlin)",
    "schedule:officeHours",
    "schedule:automergeOfficeHours",
    ":semanticCommits",
    ":label(renovate)",
    ":enableVulnerabilityAlerts"
  ],
  "rebaseWhen": "conflicted"
}
```

This configuration includes:
- Renovate's recommended configuration
- Automatic merging of patch updates
- PR assignment to a specified user (automatically set using the arg0 parameter)
- European timezone and office hours scheduling
- Semantic commit messages
- Renovate labeling
- Vulnerability alerts
- Conflict-only rebasing strategy

**Usage:**

```json
{
  "extends": ["github>onelitefeathernet/renovate:default(onelitefeathernet/maintainers)"]
}
```

In this example, `onelitefeathernet/maintainers` is passed as the `arg0` parameter, which will be used to automatically set the assignee for all Renovate pull requests. You can replace it with your own username, team name, or any valid GitHub user/team identifier that should be assigned to the PRs.

### Additional Presets

More presets will be added in the future to support other package ecosystems and versioning schemes.

## Development

### Release Process

This project uses [semantic-release](https://github.com/semantic-release/semantic-release) for automated versioning and package publishing. The release process is triggered automatically on push to main branches.

The release configuration uses:
- Conventional Commits for commit message parsing
- Automated release notes generation
- Git and GitHub integration

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
