---
name: ext-ds-php
description: Guides PHP developers in choosing and using ext-ds data structures idiomatically instead of arrays or SPL collections. Use when working with PHP ext-ds, Ds\\Vector, Ds\\Map, Ds\\Set, Ds\\Stack, Ds\\Queue, Ds\\Deque, collection performance, or migrations from PHP arrays to typed data structures.
---

# PHP ext-ds

## Quick Start

Use `ext-ds` when code needs explicit collection semantics instead of generic PHP arrays. Check the target project's `ext-ds` major version first; v1 and v2 are not API-compatible.

```php
use Ds\Map;
use Ds\Set;
use Ds\Vector;

$ids = new Set([1, 2, 2, 3]);
$namesById = new Map([1 => 'Ada', 2 => 'Grace']);
$orderedNames = new Vector(['Ada', 'Grace']);
```

Prefer arrays for interoperability, serialization boundaries, and small literal config. Prefer `Ds\*` types inside domain/application code when the operation model matters.

## Choose The Type

- `Ds\Vector`: ordered list with integer indexes; use for append-heavy lists and random access.
- `Ds\Deque`: ordered double-ended queue; use when pushing or shifting at both ends.
- `Ds\Map`: key-value dictionary that preserves insertion order and accepts non-string, non-int keys.
- `Ds\Set`: unique values with fast membership checks.
- `Ds\Stack`: last-in-first-out workflow.
- `Ds\Queue`: first-in-first-out workflow.
- `Ds\PriorityQueue`: priority-based processing where highest priority is consumed first.

## Workflows

### Introducing ext-ds

1. Check `composer.json`, lock files, CI images, or `php --ri ds` to identify whether the project targets `ext-ds` v1 or v2.
2. Declare the chosen major in runtime `composer.json` when production code depends on `Ds\*`, for example `"ext-ds": "^2.0"`.
3. Replace arrays only where an invariant becomes clearer: uniqueness, FIFO/LIFO, priority, map key identity, or list operations.
4. Keep external boundaries array-friendly: HTTP payloads, JSON, persistence, templates, and public APIs usually still receive or return arrays.
5. Convert at boundaries with `toArray()` or constructors.

### Replacing Arrays

Use this mapping as a default, then verify behavior:

- `array<int, T>` used as a list: `Ds\Vector`.
- `array<int|string, T>` used as a lookup table: `Ds\Map`.
- `array<T, true>` or repeated `in_array()` membership checks: `Ds\Set`.
- `array_shift()` queue behavior: `Ds\Queue` or `Ds\Deque`.
- `array_pop()` stack behavior: `Ds\Stack`.
- Sorted work items by explicit priority: `Ds\PriorityQueue`.

### Review Checklist

- The chosen type matches the actual invariant, not just performance hopes.
- Runtime `composer.json` pins the intended `ext-ds` major, such as `"^1.0"` or `"^2.0"`, when code uses `Ds\*`.
- Code does not call array-only functions on `Ds\*` objects.
- Suggested APIs are verified against the project's installed `ext-ds` major.
- Equality-sensitive code accounts for `Ds\Map` supporting object keys and preserving insertion order.
- Tests cover collection behavior, especially uniqueness, ordering, and empty collection handling.

## Examples

Use `Set` for explicit uniqueness:

```php
use Ds\Set;

$seenIds = new Set();

foreach ($events as $event) {
    if ($seenIds->contains($event->id)) {
        continue;
    }

    $seenIds->add($event->id);
    handle($event);
}
```

## Composer Installation

Install `netresearch/composer-agent-skill-plugin`, then install `simpod/skill-ext-ds`. The plugin discovers this root `SKILL.md` from the package type `ai-agent-skill`.
