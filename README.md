---
type: Bundle Guide
title: Network Engineering Knowledge Base
description: A worked Open Knowledge Format 0.1 example for network engineering knowledge.
tags: [okf, example, networking, knowledge-base]
timestamp: 2026-07-02T00:00:00Z
---

# Network Engineering Knowledge Base

This repository is a worked example of an [Open Knowledge Format (OKF) 0.1](index.md) bundle. It represents network designs, standards, runbooks, API guidance, and configuration examples as plain Markdown documents with YAML frontmatter.

The content is fictional and intended for demonstration. Do not apply the example configurations directly to production networks.

## What you need

Nothing beyond a text editor is required. Every concept is readable Markdown, and its metadata is ordinary YAML.

Optional tools include:

* [Git](https://git-scm.com/) to clone and version the bundle.
* A Markdown viewer, such as GitHub or an editor preview.
* A YAML parser for automated indexing, filtering, or retrieval.

There is no required OKF SDK, schema registry, database, or hosted service.

## Walkthrough

1. Start with the root [index](index.md), which declares the OKF version and lists the available knowledge areas.
2. Choose an area such as [designs](designs/). Each directory index reveals the next useful layer without requiring a reader or agent to load the whole repository.
3. Open a concept such as the [data-center fabric HLD](designs/high-level/dc-fabric.md).
4. Read its YAML frontmatter to classify and filter it. The required `type` identifies the concept kind; fields such as `description`, `tags`, `owner`, and `status` add context.
5. Read the Markdown body for the actual knowledge, then follow links to related designs, standards, examples, and runbooks.
6. Consult [log.md](log.md) for the bundle's chronological update history.

In compact form:

```text
index.md
  -> designs/index.md
    -> designs/high-level/index.md
      -> designs/high-level/dc-fabric.md
        -> standards/network.md
        -> operations/network-runbooks.md
```

## Repository layout

```text
.
├── README.md
├── index.md
├── log.md
├── apis/
├── designs/
│   ├── high-level/
│   └── low-level/
├── examples/
├── operations/
└── standards/
```

`index.md` and `log.md` are reserved OKF filenames. Every other Markdown file is a concept document and therefore includes YAML frontmatter with a non-empty `type`.

## Adding knowledge

1. Create a Markdown file in the most appropriate directory.
2. Add YAML frontmatter containing at least `type`; `title`, `description`, `tags`, and `timestamp` are recommended.
3. Write the concept body using clear headings, tables, lists, and fenced examples.
4. Link related concepts using standard relative Markdown links.
5. Add the concept to its directory's `index.md`.
6. Record a meaningful bundle change in `log.md`.

Unknown metadata fields are allowed, so producers can extend concepts without requiring a central schema change.

## Consuming the bundle programmatically

A consumer can recursively enumerate `.md` files, skip special handling for `index.md` and `log.md`, parse each concept's YAML frontmatter, and index the body as Markdown. Links form a directed knowledge graph and directory indexes provide an efficient progressive-disclosure path.

Consumers should tolerate unknown types, additional metadata fields, missing optional fields, and broken links, as required by OKF's permissive consumption model.
