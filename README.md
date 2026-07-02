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

## Keeping the bundle up to date with an agent

OKF defines the output format; it does not prescribe a particular ingestion product. In a working deployment, an enrichment agent can sit alongside a `source-docs/` directory and process new or changed files into the OKF bundle.

```text
source-docs/
    |
    | new, changed, renamed, or deleted files
    v
enrichment agent
    |-- extracts metadata and important facts
    |-- creates or updates typed concepts
    |-- adds relationships and directory index entries
    |-- records provenance and update-log entries
    |-- validates frontmatter and links
    v
OKF repository
    |
    | reviewed commit or pull request
    v
people and consumption agents
```

The agent might be triggered by a filesystem watcher, scheduled scan, Git commit, CI job, or document-system webhook. It should compare content hashes or repository history so that unchanged documents are not processed repeatedly. Renames and deletions need explicit handling to avoid stale concepts and broken links.

A practical workflow is:

1. Detect a changed source document.
2. Parse it and identify the concepts it contains.
3. Create or update the corresponding OKF documents and preserve source provenance in producer-defined metadata.
4. Refresh the appropriate `index.md` files and cross-links.
5. Add a dated entry to `log.md`.
6. Validate the bundle and open a pull request for human review.

The source documents remain the evidence; the OKF bundle is the curated, agent-friendly knowledge layer. For high-consequence material, an agent should propose changes rather than silently publishing them.

## OKF compared with vector-based RAG

OKF and retrieval-augmented generation (RAG) solve related but different problems. OKF is a portable representation and navigation convention. Vector RAG is a retrieval mechanism that embeds chunks and searches for semantically similar content. They can be used independently, but they are often strongest together.

| Area | OKF repository | Vector-based RAG |
|---|---|---|
| Primary purpose | Represent, curate, version, and exchange knowledge | Retrieve relevant passages from a large corpus |
| Storage | Markdown, YAML, directories, and links | Source content plus embeddings, chunks, and a vector index |
| Human readability | Excellent; every artifact is directly inspectable | The source is readable, but embeddings and retrieval behavior are not |
| Retrieval | Hierarchy, metadata, links, text search, and agent navigation | Semantic similarity, usually combined with filters or keyword search |
| Setup | Works with files and Git; no service is required | Requires chunking, an embedding model, an index, and retrieval logic |
| Change history | Natural Git diffs, review, attribution, and rollback | Requires coordination between source history and index refreshes |
| Portability | Clone or archive the directory | Depends on embedding model, index format, and database tooling |
| Very large corpora | Needs disciplined hierarchy, generated indexes, or an added search layer | Designed to narrow large corpora to a small set of candidate chunks |
| Retrieval failure mode | A consumer may miss a concept because navigation or metadata is weak | Relevant chunks may not rank highly, or chunks may lose surrounding context |
| Best fit | Curated, durable, shared knowledge | Broad, high-volume, or loosely structured source collections |

### Advantages of OKF

* Knowledge is transparent, diffable, reviewable, and usable offline.
* Teams can exchange one predictable format instead of every agent inventing its own metadata and folder conventions.
* Relationships and context are curated explicitly rather than inferred only at query time.
* A bundle remains useful without a particular model, vector database, or vendor.
* Git provides a straightforward governance path through branches, pull requests, ownership, and audit history.

### Limitations of OKF

* It does not provide semantic search by itself.
* Quality depends on useful concepts, descriptions, indexes, and cross-links.
* An agent or person must keep the curated layer synchronized with its sources.
* Poorly organized repositories can force a consumer to inspect too many files.
* Plain-text knowledge requires normal repository access controls; placing sensitive content in Markdown does not make it safe automatically.

### Advantages and costs of vector RAG

Vector RAG can find conceptually related passages even when the query and source use different words. That becomes valuable when documents number in the thousands or millions and users cannot predict where an answer lives. It also lets the model receive a small set of retrieved chunks instead of the entire corpus.

The tradeoff is additional machinery: documents must be parsed and chunked, chunks embedded, metadata indexed, and the index refreshed when sources change. Retrieval must be evaluated and tuned. A vector database can return a plausible passage without the wider document context, and its contents are harder for a person to inspect or exchange than a directory of Markdown files.

## Token usage

Neither approach makes model tokens free; they spend them at different points.

For an agent-maintained OKF bundle:

* Initial enrichment may use generation tokens to read source documents and produce curated concepts.
* Incremental processing should spend tokens only on changed documents and any affected indexes or links.
* At question time, progressive disclosure lets an agent read a small index, inspect frontmatter, and open only the most relevant concepts.
* If navigation is poor, discovery can degrade into scanning metadata—or even bodies—from many files, increasing token use substantially.

For vector RAG:

* Initial ingestion incurs embedding work across the chunked corpus, followed by incremental embedding for changes.
* Each query incurs retrieval and usually passes only the top matching chunks to the generation model.
* Query-time context can therefore remain fairly stable as the corpus grows, although increasing the number or size of retrieved chunks raises generation-token use.
* Bad chunking or weak retrieval can save tokens while omitting the evidence needed for a correct answer.

A useful mental model is:

```text
OKF query context ~= indexes inspected + metadata inspected + concepts opened
RAG query context ~= query/retrieval overhead + retrieved chunks
```

Exact costs depend on document size, model tokenizer, chunking, retrieval depth, and how much context the agent chooses to open. The format alone cannot guarantee a particular token saving.

## How it scales

There is no hard OKF document limit. A well-structured bundle can contain thousands of concepts, but scale changes what supporting capabilities are sensible.

| Corpus shape | Practical approach |
|---|---|
| Tens to hundreds of curated concepts | Plain OKF hierarchy, indexes, links, and normal text search |
| Thousands of concepts | Generated indexes, consistent metadata, bounded directory sizes, validation, and metadata/full-text search |
| Tens of thousands or highly variable documents | Use OKF as the governed knowledge layer and add a search or vector retrieval index |
| Very large, rapidly changing raw corpus | Use RAG for discovery; promote durable, reviewed knowledge into OKF |

A single flat `index.md` containing thousands of entries merely moves the scaling problem into one large prompt. Prefer several meaningful levels, concise descriptions, and generated indexes. Consumers can also build a local catalog from frontmatter without changing the underlying OKF files.

The most robust large-scale pattern is often hybrid:

1. Keep original documents as the evidence layer.
2. Maintain important, reusable knowledge as reviewed OKF concepts.
3. Index either or both layers for full-text and vector retrieval.
4. Return retrieved OKF concepts with their links and metadata so the agent can expand context deliberately.

## Team and organizational use cases

OKF is particularly useful as a team standard. Instead of different agents producing incompatible JSON files, private vector indexes, ad hoc Markdown, or tool-specific databases, team members can require knowledge deliverables to use the same minimal conventions.

Example uses include:

* Passing a project knowledge bundle to another engineer, team, supplier, or agent.
* Standardizing the output of documentation and enrichment agents.
* Keeping architecture decisions, standards, runbooks, and examples connected.
* Reviewing AI-generated knowledge through ordinary pull requests.
* Shipping domain knowledge alongside code without requiring access to a central service.
* Creating a durable curated layer above wikis, PDFs, tickets, API specifications, and operational records.
* Seeding a future RAG system with cleaner documents and stronger metadata.

An organization can standardize the required `type` field and a small recommended metadata vocabulary while still allowing each domain to add its own fields. This gives agents a predictable interchange format without forcing every team into the same taxonomy or software stack.

OKF is less compelling when the only need is transient question answering over a huge, fast-changing corpus and nobody intends to curate, review, exchange, or retain the resulting knowledge. In that case, RAG may be the more direct starting point.

## Consuming the bundle programmatically

A consumer can recursively enumerate `.md` files, skip special handling for `index.md` and `log.md`, parse each concept's YAML frontmatter, and index the body as Markdown. Links form a directed knowledge graph and directory indexes provide an efficient progressive-disclosure path.

Consumers should tolerate unknown types, additional metadata fields, missing optional fields, and broken links, as required by OKF's permissive consumption model.
