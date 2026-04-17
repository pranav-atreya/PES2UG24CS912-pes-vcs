# PES-VCS — A Minimal Version Control System

## Overview

PES-VCS is a simplified version control system built from scratch as part of the Operating Systems course. It mimics the core ideas behind Git, including content-addressable storage, staging, and commit history.

The system stores complete snapshots of a project instead of diffs, ensuring data integrity and efficient storage using SHA-256 hashing.

---

## Features

* **Content-addressable storage**

  * Files are stored using SHA-256 hashes
  * Identical content is stored only once (deduplication)

* **Object types**

  * Blob → file contents
  * Tree → directory structure
  * Commit → project snapshot with metadata

* **Staging Area (Index)**

  * Tracks files to be included in the next commit
  * Detects modified, deleted, and untracked files

* **Commit System**

  * Creates snapshots of the project
  * Maintains history using parent-linked commits

---

## Project Structure

```
.pes/
├── objects/          # Stores blobs, trees, commits
├── refs/
│   └── heads/
│       └── main      # Current branch reference
├── index             # Staging area
└── HEAD              # Points to current branch
```

---

## Commands Implemented

| Command               | Description            |
| --------------------- | ---------------------- |
| `pes init`            | Initialize repository  |
| `pes add <file>`      | Stage files            |
| `pes status`          | Show file status       |
| `pes commit -m "msg"` | Create commit          |
| `pes log`             | Display commit history |

---

## Implementation Details

### Object Storage (`object.c`)

* Stores objects in `.pes/objects/`
* Uses SHA-256 hashing
* Ensures atomic writes using temp files

### Tree Construction (`tree.c`)

* Serializes directory structure
* Ensures deterministic ordering

### Index (`index.c`)

* Text-based staging system
* Tracks file metadata (mtime, size, hash)

### Commit System (`commit.c`)

* Creates commit objects
* Links commits using parent pointers
* Updates HEAD reference

---

## Build Instructions

```bash
make
```

---

## Testing

### Phase 1

```bash
make test_objects
./test_objects
```

### Phase 2

```bash
make test_tree
./test_tree
```

### Integration Test

```bash
make test-integration
```

---

## Learning Outcomes

* Understanding of filesystem-based version control
* Implementation of content-addressable storage
* Use of hashing for integrity and deduplication
* Practical exposure to Git internals

---

## Author

Pranav Atreya
SRN: PES2UG24CS912
