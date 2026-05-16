# Contributing

Thanks for considering a contribution. A few ground rules to set expectations.

## Before opening a PR

**Open an issue first for any structural change.** The framework is intentionally opinionated — every layer exists because of a corresponding failure mode. Structural PRs need to start from the failure they address, not from "I think this would be nicer."

Examples of changes that should come with an issue first:

- Adding or removing a layer.
- Changing a core constraint (e.g., "Project Agents are read-only").
- Renaming or reorganizing memory tiers.
- Changing the L1 / L2 / L3 separation.
- Replacing the Hub-and-Spoke topology.

Examples of changes that can be PRs directly:

- Translations and language polish.
- Typos, dead links, formatting fixes.
- Documentation clarifications (without changing meaning).
- New FAQ entries answering real questions you have been asked.
- Glossary additions for terms used but not yet defined.

## PR guidelines

- Keep the diff focused. One concept per PR.
- For new content, prefer **distilling** over **expanding**. The document's goal is to stay close to lived experience, not to grow indefinitely.
- For Traditional Chinese ↔ English sync: when editing one, also update the other if the change is content-bearing (not just typos).
- If your PR adds a self-learning rule derived from your own experience, please attribute the failure mode it came from (anonymized is fine).

## What I will not merge

- Pure expansion of layer counts, rule categories, or terminology without a concrete reason.
- Vendor-specific implementation details framed as required (those belong in Layer F as **illustrative**, not normative).
- Content that re-introduces identifiable internal details from any specific organization.
- Speculative future-proofing without a real adoption story behind it.

## Reporting failure modes

Issues are very welcome — especially *"I hit X, the framework does not address it."* Even if a particular issue does not result in a PR, it shapes the next revision.

When reporting:

- Describe the failure mode concretely.
- Anonymize any organization or product names.
- Note which layer (A–F) you think it belongs to, if any.
- If you found a workaround, share it.

## Security

For security-sensitive findings (e.g., an example pattern in the docs that would leak data if followed literally), please follow [SECURITY.md](./SECURITY.md) instead of opening a public issue.

## Code of conduct

Be civil. Disagreements about framework design are expected and welcome; personal attacks are not. Comments that would be embarrassing to read back in a year are unlikely to land well in the first place.

## License

By contributing, you agree your contribution will be licensed under the same [CC BY 4.0](./LICENSE) terms as the rest of the documentation.
