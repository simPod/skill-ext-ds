# simpod/skill-ext-ds

AI agent skills for PHP `ext-ds`.

This repository contains two skills:

- `php-ext-ds-v1`: `ext-ds:^1` API notes.
- `php-ext-ds-v2`: `ext-ds:^2` API notes.

## Install

With `skills`:

```sh
npx skills add simPod/skill-php-ext-ds --skill php-ext-ds-v1
npx skills add simPod/skill-php-ext-ds --skill php-ext-ds-v2
```

With `dotagents`:

```sh
npx @sentry/dotagents init
npx @sentry/dotagents add simPod/skill-php-ext-ds --name php-ext-ds-v1
npx @sentry/dotagents add simPod/skill-php-ext-ds --name php-ext-ds-v2
npx @sentry/dotagents install
```
