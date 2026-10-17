# Token Tree viewer

An interactive viewer for **empirical token trees**: thousands of completions of the same prompt, re-tokenized with the model's own tokenizer and merged into a tree that shows where the model's continuations branch and where they converge. No logprobs are needed.

This repo holds only the **built** viewer and its data. It's served at [ulyssespascal.com/apps/token-trees](https://ulyssespascal.com/apps/token-trees/) and pinned by release tag. The `tokentrees` library and the viewer source are developed separately.

## Data

There are 2,000 completions from `openai/gpt-5.4-mini` at default temperature, 1,000 for each of two prompts that differ by one word:

- *Complete the following thought: "History, written by Artificial Intelligence"*
- *Complete the following thought: "History, rewritten by Artificial Intelligence"*

The viewer shows three trees:

| Tree | What it is |
|---|---|
| **History, written and rewritten by Artificial Intelligence** | Both prompts together, keeping only the branches that reach a shared ending, so you see where the two framings converge |
| **History, written by Artificial Intelligence** | The full branching tree for "written", from opening to common endings |
| **History, rewritten by Artificial Intelligence** | The same for "rewritten" |

## Layout

```
dist/            static site (open dist/index.html via any static server)
  data/          manifest.json, one GRAPH_V1 file per tree, SEQUENCES_V1 sidecars, token index
```

All paths are relative, so `dist/` can be served from any subpath.
