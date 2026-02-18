# How to use the generated seed with Bittensor (`btcli`)

When this tool finds a vanity SS58 address, it shows the corresponding **32‑byte seed hex**.  
You can use that seed to recreate the same key on Bittensor via `btcli`.

> ⚠️ Treat the seed like a private key. Anyone with this seed can control the funds / identity for that address.

---

## 1. Regenerate a coldkey from the seed

Use `btcli wallet regen-coldkey` (or its alias `btcli w regen_coldkey`) and pass the seed hex:

```bash
btcli wallet regen-coldkey \
  --wallet-name my_wallet \
  --seed 0xYOUR_32_BYTE_SEED_HEX
```

If you omit `--seed`, `btcli` will ask interactively whether to use **mnemonic**, **seed hex string**, or **JSON file** and you can paste the seed when prompted.

Once regenerated, the coldkey’s SS58 address should match the vanity address you saw in the finder.

---

## 2. Regenerate a hotkey from the seed

Similarly, you can regenerate a **hotkey**:

```bash
btcli wallet regen-hotkey \
  --wallet-name my_wallet \
  --hotkey my_hotkey_name \
  --seed 0xYOUR_32_BYTE_SEED_HEX
```

Again, if you run it without `--seed`, `btcli` will prompt you and you can choose the seed‑hex option.

---

## 3. Official `btcli` documentation

For full details, options, and security notes, see the official Bittensor CLI docs:

- `btcli wallet regen-coldkey`: [`https://docs.learnbittensor.org/btcli#btcli-wallet-regen-coldkey`](https://docs.learnbittensor.org/btcli#btcli-wallet-regen-coldkey)
- `btcli wallet regen-hotkey`: same section in the `btcli` reference.

