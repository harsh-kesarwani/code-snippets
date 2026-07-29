# DSA Templates

Reusable C++ templates for common DSA topics. Each template lists its complexity, a short note on when to use it, and a code snippet.

## Structure

- Templates are grouped by topic, one folder per topic.
- One Markdown file per template; related variants live in the same file.
- The [Index](#index) below links to every template.

## Conventions

Follow these so templates stay consistent (also for AI agents editing this repo):
- C++ snippets in ` ```cpp ` blocks (for highlighting).
- Placeholders are always **comments**: `// process node` on its own line, `/* condition */` inline. Keep them lowercase.
- New template: add `topic/name.md` and link it in the Index.

## Index

### Graphs
- [BFS](graphs/bfs.md)
- [DFS](graphs/dfs.md)

### Trees (Binary)
- [BFS](trees/bfs.md)
- [DFS](trees/dfs.md)

### Arrays
- [Prefix / Suffix Arrays](arrays/prefix_suffix.md)

### Searching
- [Binary Search](searching/binary_search.md)

### Math
- [Sieve of Eratosthenes](math/sieve_of_eratosthenes.md)
- [SPF Array (Smallest Prime Factor)](math/smallest_prime_factor.md)
- [GCD - Euclidean Algorithm](math/gcd.md)
- [nCr (Modular)](math/ncr_mod.md)

### Backtracking
- [Backtracking](backtracking/backtracking.md)
