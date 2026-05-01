# simpod/skill-ext-ds

Composer-distributed AI agent skill for using PHP `ext-ds` collection types idiomatically.

## Install

Install the Composer agent skill plugin in the consuming project:

```sh
composer require netresearch/composer-agent-skill-plugin
```

Install this skill package:

```sh
composer require simpod/skill-ext-ds
```

The package is type `ai-agent-skill`, so the plugin discovers the root `SKILL.md` automatically.

## Contents

- `SKILL.md`: agent instructions for choosing and using `Ds\Vector`, `Ds\Map`, `Ds\Set`, `Ds\Stack`, `Ds\Queue`, `Ds\Deque`, and `Ds\PriorityQueue`.
- `composer.json`: Composer package metadata for Packagist distribution.
