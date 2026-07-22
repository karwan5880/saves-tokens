# Skillreaper

**Type:** local configuration/transcript auditor. **Repository:** [thousandflowers/skillreaper](https://github.com/thousandflowers/skillreaper). **License:** MIT.

## Method

Skillreaper inventories skills, agents, and MCP servers, then compares their always-visible configuration cost with evidence of actual use in local Claude Code transcripts. It reports candidates for reversible pruning rather than compressing task content.

## Evidence and cautions

The author and community posts report installations carrying thousands of estimated tokens in unused descriptions. This is a **project/community claim**, and character-to-token estimates vary by tokenizer and content. The core value is evidence-based inventory rather than a universal percentage.

A component unused in historical transcripts may still be necessary later. Inspect the proposed changes, back up configuration, and compare `/context`, `/usage`, task success, and provider billing before and after pruning.

## Sources

- [Repository](https://github.com/thousandflowers/skillreaper)
- [Go package documentation](https://pkg.go.dev/github.com/thousandflowers/skillreaper)
