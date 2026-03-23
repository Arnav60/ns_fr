# BOLA Attack Simulation and Mitigation Using OWASP Juice Shop

**CS 6415: Network Security — University of New Brunswick**  
**Author:** Arnav S Awasthi

---

## Overview

This repository contains the written report for a hands-on simulation of Broken Object Level Authorization (BOLA), the number one vulnerability in the OWASP API Security Top 10. The project demonstrates how BOLA can be exploited against OWASP Juice Shop in an isolated lab environment, and implements two combined mitigations: server-side ownership validation and UUID-based ID replacement.

---

## What the Project Covers

### Attack
- Set up a two VM isolated lab (Kali Linux attacker + Ubuntu target) in VirtualBox
- Deployed OWASP Juice Shop via Docker on the target VM
- Used Burp Suite to intercept HTTP traffic and manipulate basket IDs in the API request
- Successfully accessed victim user basket data using only a valid attacker JWT and a modified URL parameter

### Mitigation
Two fixes were implemented in a locally cloned and patched version of Juice Shop, run simultaneously on a separate port for direct before-and-after comparison:

1. **Server-side ownership validation** — added to `routes/basket.ts`, compares the basket's registered owner against the authenticated user ID extracted from the JWT, returns 403 Forbidden on any mismatch
2. **UUID-based IDs** — added to `models/basket.ts`, replaces sequential integer basket IDs with randomly generated UUIDs to prevent enumeration

---

## How to Run

### Vulnerable instance (for attack demo)
```bash
docker run -d -p 3000:3000 bkimminich/juice-shop
```

### Patched instance (for mitigation demo)
```bash
git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
npm install
npm install uuid
npm install --save-dev @types/uuid
PORT=3001 npm start
```

Apply the changes to `routes/basket.ts` and `models/basket.ts` as described in Section III-F of the report before starting.

---

## Report

The full report is written in IEEE two-column format using IEEEtran. To compile:

```bash
pdflatex ns_draft7.tex
```

Or paste the contents into [Overleaf](https://www.overleaf.com) with the IEEEtran class and compile there.
