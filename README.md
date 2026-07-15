<div align="center">

# Spark

**A local-first second brain that catches the thought before it disappears.**

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet)](https://dotnet.microsoft.com/)
[![.NET MAUI](https://img.shields.io/badge/.NET_MAUI-mobile--first-512BD4?logo=dotnet)](https://learn.microsoft.com/dotnet/maui/)
[![SQLite](https://img.shields.io/badge/SQLite-local--first-003B57)](https://www.sqlite.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

</div>

---

## Overview

Most good ideas don't show up when you're sitting down to write — they show up mid-page in a book, on a walk, half-asleep, and they're gone thirty seconds later because writing them down properly takes too many steps.

Spark captures the thought the instant it hits, raw, by voice or text, tied to whatever you were reading at the time. In the background, it compares that thought against everything you've captured before and surfaces real connections — not shared keywords, but *this confirms*, *this contradicts what you said in March*, *this is the same idea from a different angle*. You decide which ones are real. Over time it becomes an archive of your own thinking, ready to turn into an essay, an article, or just a clearer picture of what you actually believe.

---

## Example

<div align="center">
<img src="docs/screenshot-graph.png" alt="Connections view" width="500"/>

<sub>Captured thoughts, linked and labeled by relationship.</sub>
</div>

---

## Features

- Capture by voice or text, stored exactly as said — never rewritten or polished by AI
- Every thought anchored to its source (book, page, moment)
- AI-suggested connections, labeled by relationship: confirms, contradicts, nuances, builds on
- Nothing links automatically — every connection is approved by you
- Writing mode: pulls your own validated thoughts into an outline when you're ready to write
- Local-first storage — your data stays on your machine

---

## Tech Stack

| Component | Detail |
|---|---|
| Language | C# on .NET 8+ |
| UI | .NET MAUI (mobile-first: iOS + Android) |
| Storage | Entity Framework Core + SQLite, fully local |
| AI | Embeddings + LLM API — used for finding and classifying connection |

---

## Getting Started

```bash
git clone https://github.com/<your-username>/spark.git
cd spark
dotnet run
```

---

## License

MIT — see [LICENSE](LICENSE).
