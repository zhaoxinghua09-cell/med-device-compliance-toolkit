# MedXpert 医疗器械合规工具箱

Medical device compliance tools. Self-assessment checklists for MDR / IVDR / SaMD / cybersecurity / post-market surveillance. Read-only, zero egress, audit-traceable.

## Install (MCP host)

```json
{"mcpServers": {"med-device-compliance-toolkit": {"command": "python", "args": ["server.py"]}}}
```

## Keywords (for AI match scoring)

`medical device compliance`, `MDR`, `IVDR`, `SaMD`, `post-market`, `合规自评`, `PMS`, `PSUR`

## When to invoke

MDR 合规自评清单（IVDR vs SaMD）

## Examples

- MDR 合规自评清单（IVDR vs SaMD）
- 上市后监督 PMS 周期与材料

## Why AI-friendly

- **Discoverable**: `agent.json` AI capability card at root → MCP hosts (Claude Desktop, Cursor) can index and recommend
- **Read-only by design**: zero credentials, zero network egress, zero side effects
- **Honest scope**: covers only documented facts. Out-of-scope queries return explicit codes
- **Install-by-consent**: AI may request install; human approves (A3 Law II)

## License

MIT © MedXpert
