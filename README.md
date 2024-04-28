# Solana ED25519 Signature Verification Helper Function

Pretty self-explanatory. Quite a bit more expensive than the precompile program,
but also quite a bit easier to use with no ix sysvar shenanigans necessary.

--- 

## Compute Costs

See [compute-usage.csv](compute-usage.csv) or look at the chart below for the compute costs per message length.

There's a static cost of ~11,000 CUs for curve stuff, and an additional cost of
~8000 CUs per SHA512 128 byte block. There's an 80 byte overhead from the signature R scalar, pubkey scalar,
and 16 byte message length, which is why the second block starts at only 48 message bytes.

Formula is approximately: `CU_COST = ceil((80 + MESSAGE_BYTE_LEN) / 128) * 8000 + 11000`

![compute-usage.png](compute-usage.png)