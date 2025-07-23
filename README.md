# Global Notarization Workflow

This repository hosts a **centralized GitHub Action** that automatically notarizes all of my connected repositories every time code is pushed.  
It ensures that every project is **cryptographically timestamped, verifiable, and backed up** — even if a repo is cloned, mirrored, or taken offline.

## What It Does
On every push to a linked repository, this workflow:
1. Creates a compressed snapshot (`snapshot.tar.gz`) of the entire repo.
2. Generates a **SHA-256 hash** of that snapshot.
3. Timestamps the hash on **Bitcoin** using [OpenTimestamps](https://opentimestamps.org) (immutable proof of existence).
4. Uploads the snapshot to **IPFS** (distributed, content-addressed storage).
5. Updates or creates a `PROOF.md` file with:
   - SHA-256 hash of the repo snapshot  
   - Bitcoin timestamp proof (`.ots` file)  
   - IPFS content ID (CID)  
6. Commits and pushes the proof files back to the repo automatically.

## Why It Exists
This system ensures that **all of my work remains protected**, provably mine, and independently verifiable — even if:
- A repository is cloned, copied, or deleted.
- A third party disputes authorship.
- GitHub or any single service goes offline.

By maintaining a **cryptographic chain of evidence** across multiple systems (Bitcoin, IPFS, and GitHub), this workflow creates **tamper-proof proof of authorship and ownership** for all of my active repositories.

## How to Use It
To connect any of my repositories:
1. Add a simple pointer workflow:
   ```yaml
   name: Use Global Notarization

   on:
     push:
       branches:
         - main

   jobs:
     notarize:
       uses: YOUR_USERNAME/global-notarization/.github/workflows/notarize.yml@main
