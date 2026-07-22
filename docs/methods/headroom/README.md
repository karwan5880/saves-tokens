# Headroom

**Type:** third-party API/context compression proxy. **Repository:** [chopratejas/headroom](https://github.com/chopratejas/headroom).

## Method

The proxy sits between a coding client and provider API, attempting to compress context/payloads before requests are sent.

## Cautions

A proxy can receive proprietary prompts, code and credentials; it can also change prompt-cache behavior, tool protocols, and debugging semantics. Its local “saved tokens” is not the provider bill. Review source, data flow, endpoint/TLS configuration, and service terms before use; compare provider-billed totals and task outcomes.

## Source

- [Repository](https://github.com/chopratejas/headroom)
