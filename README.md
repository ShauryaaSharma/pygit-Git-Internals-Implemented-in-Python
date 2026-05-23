# pygit — Git Internals Implemented in Python

A minimal Git client built from scratch in Python using only the standard library. Implements core Git internals — object hashing, index parsing, tree and commit writing, and pack file pushing over HTTP Smart Protocol. Supports `init`, `add`, `commit`, `diff`, `status`, and `push` to GitHub.


---

## What it does

pygit implements just enough of Git to:

- Initialize a local repository
- Stage files to the index
- Commit snapshots to the master branch
- Push commits to a real remote server (GitHub, Bitbucket, etc.)
- Show file status and diffs between the index and working copy

---

## How it works

Git's object model is built on three core object types stored in `.git/objects/`:

| Object | Description |
|--------|-------------|
| **blob** | A file's raw contents |
| **tree** | A snapshot of a directory (lists blobs and sub-trees) |
| **commit** | Points to a tree, a parent commit, author, and message |

Each object is SHA-1 hashed, zlib-compressed, and written to `.git/objects/ab/cdef...`.

pygit implements:

- **Object store** — hashing, reading, and writing blobs, trees, and commits
- **Index parsing** — reading and writing the binary `.git/index` file
- **Pack files** — encoding and sending missing objects over HTTP Smart Protocol
- **pkt-line format** — Git's length-prefixed packet format for server communication

---

## Requirements

- Python 3.5+
- No external dependencies — standard library only

---

## Installation

```bash
git clone https://github.com/yourusername/pygit.git
cd pygit
```

---

## Usage

### Initialize a repo
```bash
python pygit.py init myrepo
cd myrepo
```

### Stage files
```bash
python pygit.py add file.py
```

### Check status
```bash
python pygit.py status
```

### View diff
```bash
python pygit.py diff
```

### Commit
```bash
python pygit.py commit -m "Your commit message"
```

### Push to GitHub
```bash
python pygit.py push https://github.com/username/repo.git
```

> You will be prompted for your GitHub username and password (or personal access token).

---

## Commands

| Command | Description |
|---------|-------------|
| `init <repo>` | Initialize a new repository |
| `add <paths>` | Add files to the index |
| `status` | Show changed, new, and deleted files |
| `diff` | Show diff between index and working copy |
| `commit -m <msg>` | Commit current index to master |
| `cat-file <mode> <hash>` | Inspect a Git object |
| `ls-files` | List files in the index |
| `hash-object <path>` | Hash and optionally store a file |
| `push <url>` | Push master branch to remote |

---

## Project Structure

```
pygit/
├── pygit.py       # Full implementation 
├── LICENSE.txt    # MIT License
└── README.md
```

---

## License

MIT License — see [LICENSE.txt](LICENSE.txt) for details.  
