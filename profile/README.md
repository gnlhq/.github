## GNL

A durability layer for [Vercel AI SDK](https://ai-sdk.dev) agents. It wraps `generateText` and
`streamText` and adds a journal, so a side-effecting tool call is never silently run twice — not
after a crash, not after a retry, not when the model plans the same call again under a new id.

```ts
const chargeCard = gnlTool(tool({ /* your AI SDK tool */ }), {
  sideEffect: true,     // never replayed from the journal
  idempotency: 'args',  // never re-run when the model re-plans it with the same arguments
});

await runDurable({ runId: 'order-123', journal, model, tools: { chargeCard }, prompt });
// Crash, then call again with the same runId: finished steps replay, the card is not charged twice.
```

- **Site and docs:** [gnl.dev](https://gnl.dev)
- **Code:** [gnlhq/gnldev](https://github.com/gnlhq/gnldev) — TypeScript, Apache-2.0, on npm as `@gnldev/*`
- **First contribution:** issues labelled [good first issue](https://github.com/gnlhq/gnldev/issues?q=is%3Aopen+label%3A%22good+first+issue%22), and [Discussions](https://github.com/gnlhq/gnldev/discussions) for questions
