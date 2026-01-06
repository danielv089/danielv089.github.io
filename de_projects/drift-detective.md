---
layout: default
title: Drif Detective
nav_order: 2
---


# Drift Detective 🕵️‍♂️📊

[![Static Badge](https://img.shields.io/badge/Open%20GitHub%20Repository-blue?style=for-the-badge&logo=github)](https://github.com/danielv089/drift-detective/tree/main)

“Did the structure of my data change, and should I care?”

Drift Detective is a Python library for tracking schema evolution and detecting structural drift in tabular datasets using versioned JSON snapshots.

It is designed for data workflows where table schemas evolve over time.

The library focuses on schema-level changes and not row-level.

The current stable version of the package can be downloaded from PyPI, while the repository is actively under development.

[![Static Badge](https://img.shields.io/badge/Drift%20Detective%20PyPI-blue?style=for-the-badge&logo=python&logoColor=yellow)
](https://pypi.org/project/drift-detective/0.1.0/)

[![Static Badge](https://img.shields.io/badge/Documentation-blue?style=for-the-badge)
](https://github.com/danielv089/drift-detective/blob/main/docs/DOCUMENTATION.md)

[![Static Badge](https://img.shields.io/badge/changelog-blue?style=for-the-badge)
](https://github.com/danielv089/drift-detective/blob/main/docs/CHANGELOG.md)

## Key Features

- JSON snapshot-based schema tracking
- Added and removed column detection 
- Historical timeline of schema evolution
- Structured (dictionary) and human-readable reports
- JSON file based design (no database backedn required)
- Comprehensive schema evolution report

## Use cases

- Tracking table evolution over time
- Auditable history of schema changes
- Lightweit detection

## API Reference

Drift Detective is built around four core components, each responsible for a specific part of schema tracking and reporting:

- DfSnapshot: Captures the schema state of a pandas DataFrame at a specific point in time and stores it as a versioned snapshot.
- SnapshotHistory: Creates a schema evolution timeline listing version and schema changes.
- SnapshotDiff: Compares schema changes between two snapshot versions, listing all added and removed columns across intermediate versions.
- SchemaReport: Integrates all components into a complete report to tell the full story

Each snapshot is stored as a JSON file containing metadata and schema information:

```json
{
    "table_name": "netflix_titles",
    "filepath": "netflix_titles.csv",
    "timestamp": "20251230_161527",
    "version": 1,
    "column_count": 12,
    "row_count": 8807,
    "schema": {
        "show_id": "object",
        "type": "object",
        "title": "object",
        "director": "object",
        "cast": "object",
        "country": "object",
        "date_added": "object",
        "release_year": "int64",
        "rating": "object",
        "duration": "object",
        "listed_in": "object",
        "description": "object"
    },
    "columns_added": [],
    "columns_removed": []
}
```

You can print a human-readable timeline of all schema versions.

```bash
Snapshot Timeline for table: netflix_titles
────────────────────────────────────────────────────────────

v1  ●  20251230_162126
    │ columns: 12
    │ rows: 8807
    │ initial snapshot

v2  ●  20251230_163649
    │ columns: 11
    │ rows: 8807
    │ - removed columns: title

v3  ●  20251230_163729
    │ columns: 10
    │ rows: 8807
    │ - removed columns: listed_in
────────────────────────────────────────────────────────────
```

Drift Detective allows you to compare any two schema versions:

```bash
Snapshot Diff for table: netflix_titles
───────────────────────────────────────────────────────
Old snapshot v1  ●  20251230_162126
New snapshot v3  ●  20251230_163729
Added columns (new → old): No added column(s)
Removed columns (new → old): listed_in, title
───────────────────────────────────────────────────────
```

For a complete view of schema evolution you can generate a structured report.

```bash
Schema Change Report for table: netflix_titles
────────────────────────────────────────────────────────────
Snapshots directory: docs/snapshots/netflix_titles
Latest snapshot version: 3 
Available versions: 1, 2, 3
Total snapshots: 3
First snapshot Created: 20251230_162126
Latest snapshot Created: 20251230_163729
────────────────────────────────────────────────────────────

 Latest Snapshot for table: netflix_titles
────────────────────────────────────────────────────────────
v3  ●  20251230_163729
    |   columns: 10
    |   rows: 8807
    |   current columns: show_id, type, director, cast, country, date_added, release_year, rating, duration, description
    | + all added columns: 
    │ - all removed columns: title, listed_in
────────────────────────────────────────────────────────────

Snapshot Timeline for table: netflix_titles
────────────────────────────────────────────────────────────

v1  ●  20251230_162126
    │ columns: 12
    │ rows: 8807
    │ initial snapshot

v2  ●  20251230_163649
    │ columns: 11
    │ rows: 8807
    │ - removed columns: title

v3  ●  20251230_163729
    │ columns: 10
    │ rows: 8807
    │ - removed columns: listed_in
────────────────────────────────────────────────────────────


Snapshot Diff for table: netflix_titles
───────────────────────────────────────────────────────
Old snapshot v1  ●  20251230_162126
New snapshot v3  ●  20251230_163729
Added columns (new → old): No added column(s)
Removed columns (new → old): listed_in, title
───────────────────────────────────────────────────────
```

## Project Status and Roadmap

This project is in an early stage.

The core functionality for schema snapshotting, history tracking, comparison, and reporting is complete and usable.

Planned improvements:
- Add unit test for core components
- SQL snapshot support (PostgreSQL)
- Expanded documentation and examples

## 🧰 Tech Stack

- Python


## 🔗 References

- Python
https://www.python.org/doc/

- Pandas 
https://pandas.pydata.org/