## Vanity SS58 Finder (browser-only)

This repo contains a browser-based SS58 vanity address generator implemented in pure HTML + JavaScript: `ss58-generator.html`.

The page uses the Polkadot JS crypto stack (`@polkadot/util` and `@polkadot/util-crypto`) loaded from public CDNs and runs **entirely client-side** – no backend or Node.js build step is required.

---

### How it works

- Uses `@polkadot/util-crypto` to:
  - Randomly generate 32‑byte seeds (`randomAsU8a`).
  - Derive sr25519 keypairs (`sr25519PairFromSeed`).
  - Encode public keys as SS58 addresses (`encodeAddress`).
- Repeats this in a loop until:
  - An address matches the configured pattern, or
  - The configured **Max tries** limit is reached.
- Uses chunked loops so the UI remains responsive and progress can be updated.

No keys or seeds are ever sent to a server: everything happens inside your browser tab.

---

### Opening the tool (locally)

1. Make sure you have a **modern browser** (Chrome, Firefox, Edge, or Safari).
2. Open the file directly:
   - From Finder / Explorer: double-click `ss58-generator.html`, or
   - From the command line:

```bash
open ss58-generator.html        # macOS
xdg-open ss58-generator.html    # many Linux distros
```

If your browser blocks local module scripts, you can instead serve the folder with a small HTTP server (for example `python -m http.server`) and open `http://localhost:8000/ss58-generator.html`.

---

### UI fields

- **Match mode**
  - `endswith`: address must end with the given substring(s).
  - `contains`: address must contain the given substring(s) anywhere.

- **SS58 format**
  - Network prefix as an integer (e.g. `42` for generic Substrate).

- **Targets**
  - Comma-separated list of substrings you want to match.
  - Multiple targets are treated as alternatives: the search stops on the first address that matches *any* of the values.
  - Example: `GLS, TEST, 123`.

- **Match case**
  - When checked, matching is **case-sensitive**.
  - When unchecked, both address and target(s) are lowercased for comparison.

- **Max tries**
  - Safety cap on how many candidate addresses to generate in a single run.
  - Larger numbers increase the chance of finding a match but take longer.

---

### Output

When a match is found, the result panel shows:

- SS58 format and SS58 address.
- Public key (hex).
- Seed (hex, 32 bytes).
- Total tries, elapsed time, and approximate tries/sec.

> **Note:** Matching an SS58 address with a substring longer than about 3 characters can take a very large number of attempts. Increase **Max tries** accordingly and expect searches to run for longer.

You can store the **seed hex** and use it with Polkadot JS tooling or your own code to recreate the same sr25519 keypair.

If no match is found within **Max tries**, an error panel will state that no match was found.

---

### Security notes

- Everything is computed locally in your browser; there is no backend.
- Treat the displayed **seed** like any private key:
  - Do not share screenshots or copy it into untrusted apps.
  - Prefer running the page from a local file or a trusted local HTTP server.

