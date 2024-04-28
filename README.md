# Solana ED25519 Signature Verification Helper Functions

Pretty self-explanatory. Quite a bit more expensive than the precompile program,
but also quite a bit easier to use with no ix sysvar shenanigans necessary.

--- 

## Compute Costs

See [compute-usage.csv](compute-usage.csv), or just look at the chart directly below for the compute costs per message
length.

There's a static cost of ~11,000 CUs on Curve operations, and an additional cost of ~8000 CUs per SHA512 128 byte
block. There's an 80 byte overhead from the signature R scalar, pubkey scalar, and 16 byte message
length, which is why the second block starts at only 48 message bytes.

Formula is approximately `CU_COST = 62 * MESSAGE_BYTE_LENGTH + 20_000`

![compute-usage.png](compute-usage.png)