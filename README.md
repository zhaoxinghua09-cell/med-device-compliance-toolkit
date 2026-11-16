# 医疗器械合规工具箱（MedCompliance Toolkit）

> **Status: this pack is an expert/agent card, not a server — and the connector it depends on exists.**
> `medxpert-ortho-mcp` is published on PyPI and in the official MCP Registry, and a real `uvx` handshake
> returns its 8 tools. Install it:
>
> ```bash
> uvx medxpert-ortho-mcp
> ```
>
> **The version number is deliberately not written here.** It changed twice in one day; a number frozen in
> a card goes stale without anyone noticing. Ask the registry instead
> (`io.github.zhaoxinghua09-cell/medxpert-ortho-mcp`), or just run the install line above.
>
> The tools run on illustrative sample data and mark every result `sample_data: true`. Point
> `ORTHO_DATA_DIR` at your own datasets for real work, and run
> `python -m medxpert_ortho.server --validate-data` first — it fails loudly on a wrong path, a broken JSON
> file or a structurally bad dataset rather than quietly answering from the samples.
>
> This repository still ships no `server.py`: it is a card that a host loads, and the capability lives in
> the connector.
>
> **状态：本包是专家/Agent 卡片，不是服务；它所依赖的连接器已经存在。**`medxpert-ortho-mcp` 已发布在 PyPI 与官方 MCP Registry，并由真实 `uvx` 握手验证——返回 8 个工具。安装：
>
> ```bash
> uvx medxpert-ortho-mcp
> ```
>
> **版本号有意不写在这里。** 它在一天之内变了两次；冻在卡片里的数字会悄悄过期。要版本请查 Registry（`io.github.zhaoxinghua09-cell/medxpert-ortho-mcp`），或者直接跑上面的安装命令。
>
> 工具跑在示例数据上，每个返回值都标 `sample_data: true`。正式使用请把 `ORTHO_DATA_DIR` 指向你自己的数据集，并先跑 `python -m medxpert_ortho.server --validate-data`——路径错、JSON 坏、结构不合规都会报错退出，而不是拿示例悄悄作答。
>
> 本仓仍然没有 `server.py`：它是宿主加载的卡片，能力在连接器里。

## 许可说明 · License Notice

- **权利状态**：本仓库以 **MIT 许可** 许可发布，可依该许可证条款自由使用、修改与再分发。
- **引用建议**：引用时请标注仓库名与原文链接 `https://github.com/zhaoxinghua09-cell/med-device-compliance-toolkit`
  与权利人「赵兴华 / Steven Zhao·China」。
- **品牌状态限定**：MedXpert、SynomosAI、LGD 等为相关项目标识，
  **均未申请实体注册、未申请商标注册**；出现仅作来源标识，
  不构成对法人实体或商标权的任何主张。
- **完整条款**：见仓库根目录 [LICENSE](LICENSE)。
- **联系**：zhaoxinghua06@126.com ｜ ORCID 0009-0001-0512-1237

---


> **示例数据声明**：本工具箱引用的机构 / 标准 / 报价均为配套 ortho-mcp 连接器的**示例数据**，非官方资质目录，亦不构成任何资质背书。正式委托前须向检测机构核验最新资质与报价。

一个 **MCP 工具集合门户**：把多个医械合规方向的 MCP 资产聚到一个前门，能导航、能路由、能引导安装，并为未来新增资产预留扩展位。

> 它不是"studio"开发工作台，也不是图形仪表盘——在 WorkBuddy 生态里，它形态上是**一个导航/聚合专家包**：agent 负责索引与派发，底层能力来自已安装的 MCP 连接器与专家。

## 领域覆盖（医疗器械全域框架）

本工具箱定位为**覆盖全医疗器械领域的合规工具箱**，而非单一骨科门户。当前已入驻的是
**骨科器械检测对接**方向（ortho-mcp + 检械通）；其余领域作为扩展路线图，按《扩展位》机制平滑入住。

| 资产 | 类型 | 说明 |
|---|---|---|
| **ortho-mcp**（`medxpert-ortho-mcp`） | 连接器 | 8 个骨科器械检测工具：机构匹配 / 报价 / A+B 分包 / UDI / 法规节点 …（**已入驻**） |
| **检械通**（`medical-device-testing-link`） | 专家包 | 把 ortho-mcp 编排成端到端检测对接方案（**已入驻**） |

### 领域覆盖矩阵

| 医疗器械领域 | 状态 | 说明 |
|---|---|---|
| 骨科器械检测对接 | ✅ 已入驻 | ortho-mcp 8 工具 + 检械通端到端编排 |
| 心血管器械 | 🔜 规划中 | 扩展位预留，待新增对应 MCP 资产 |
| IVD 体外诊断 | 🔜 规划中 | 扩展位预留，待新增对应 MCP 资产 |
| 影像 / 放疗设备 | 🔜 规划中 | 扩展位预留，待新增对应 MCP 资产 |
| 无菌 / 植入器械 | 🔜 规划中 | 与骨科植入部分重叠，待专项资产 |
| 注册法规通用（NMPA/FDA/EU MDR） | 🔜 规划中 | 标准解读 / 换版解读 / 到期提醒类工具 |

## 它解决什么

- **集中入口**：用户不必记住各个 MCP 工具名，问"能干什么 / 帮我找机构"即可。
- **意图路由**：单一动作（如校验 UDI）直接派发工具；完整需求（如"送检出报价"）转包给检械通编排。
- **安装引导**：底层资产缺失时，明确告诉用户先装哪一层、按什么顺序。
- **可扩展**：加新 MCP 资产只需"索引三处同步 + 依赖登记"，门户架构不动。

## 安装顺序（重要）

本工具箱的能力全部来自底层资产，**必须按顺序装**：

1. 装 **ortho-mcp 连接器**（`ortho-mcp-connector.zip`）→ 重启会话，确认 8 个工具出现。
2. 装 **检械通专家**（`medical-device-testing-link.public.zip`）。
3. 最后装 **本工具箱**（`med-device-compliance-toolkit.public.zip`）作为门户前门。

## 数据口径（必读）

ortho-mcp 的机构库（20 家）/ 标准库（43 条）/ 器械目录（18 类）/ 报价均为**示例数据**
（随包 `ortho-data.json`，可整体替换为真实数据），非真实资质。凡涉及候选榜或报价，
工具会注明「基于演示数据，正式委托前须向机构核验」。标准仅索引标准号 + 名称 + 官方来源，未内嵌受版权正文。

## 扩展新资产

见 `skills/toolkit-nav/SKILL.md` 第四节《扩展位》：在 agent 定义与 SKILL 的索引/路由表同步登记，
新连接器在 `manifest.json` 的 `dependencies.connectors` 补依赖名即可。

## 许可证

MIT · © 2026 潘布达（Buda Pan）
