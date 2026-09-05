# 医疗器械合规工具箱 · 导航技能（toolkit-nav）

本技能是「医疗器械合规工具箱」门户的导航层：索引工具箱收录的全部 MCP 能力，
提供意图路由、安装引导与扩展登记。它本身不调用工具，而是把请求派发给底层资产。

## 一、收录资产

### 1. ortho-mcp 连接器（依赖名 medxpert-ortho-mcp，8 工具）

底层 MCP stdio 服务，零依赖、本地闭环。工具清单：

- **match_labs** — 骨科/医械检测机构智能匹配。
  入参：deviceId(D01-D18) / standardIds(S01-S43) + attrs(sterile/implant/blood/metal/coating/mri) + examId(E1-E6,默认 E1) + region + rush + top(默认 5)。
  出参：候选榜（资质四态、覆盖率、报价、交期、A+B 分包方案）。
- **calc_quote** — 指定机构分项报价与交期。
  入参：labId(L01-L20) + standardIds + rush。出参：分项费用、8% 管理费、关键路径交期。
- **find_subcontract** — A+B 分包求解。
  入参：standardIds / deviceId + attrs + examId + mainLabId(可选)。出参：主检 + 分包组合、未覆盖项、降级提示。
- **get_lab** — 机构详情。
  入参：labId + includeScope。出参：CMA/CNAS 证书、健康分、覆盖范围、联系方式、冻结状态。
- **list_devices** — 18 类骨科器械目录与默认检验项目。入参：keyword + attrs。
- **list_standards** — 43 条检验标准检索（GB/YY/ISO/ASTM/药典）。入参：keyword + cat。
- **check_udi** — UDI(GS1) 校验位验证与 AI 串解析。入参：gtin / ai。
- **list_deadlines** — 医械法规节点（GMP2025 / EU MDR-IVDR）与紧急度分级。入参：upcomingOnly。

### 2. 检械通专家（medical-device-testing-link / MedTestLink）

端到端编排 ortho-mcp：检验项目推导 → 机构匹配 → 报价交期 → A+B 分包 → 《检测对接方案》输出。
适合"我有个产品要送检"这类完整需求。

### 领域覆盖矩阵（医疗器械全域框架）

本门户定位为**覆盖全医疗器械领域的合规工具箱**，而非单一骨科门户。当前已入驻**骨科器械检测对接**
方向；其余领域为扩展路线图，按第四节《扩展位》平滑入住。

| 医疗器械领域 | 状态 | 说明 |
|---|---|---|
| 骨科器械检测对接 | ✅ 已入驻 | ortho-mcp 8 工具 + 检械通端到端编排 |
| 心血管器械 | 🔜 规划中 | 扩展位预留 |
| IVD 体外诊断 | 🔜 规划中 | 扩展位预留 |
| 影像 / 放疗设备 | 🔜 规划中 | 扩展位预留 |
| 无菌 / 植入器械 | 🔜 规划中 | 与骨科植入部分重叠 |
| 注册法规通用（NMPA/FDA/EU MDR） | 🔜 规划中 | 标准解读 / 换版 / 到期提醒 |

## 二、意图路由表

| 用户意图 | 路由目标 |
|---|---|
| 校验 / 解析 UDI | ortho-mcp · check_udi |
| 查标准号 / 送样要求 | ortho-mcp · list_standards |
| 查器械目录 / 默认项目 | ortho-mcp · list_devices |
| 查某机构资质全貌 | ortho-mcp · get_lab |
| 找机构 / 比选候选 | ortho-mcp · match_labs（或检械通端到端） |
| 算某机构报价 | ortho-mcp · calc_quote |
| 一家接不全要分包 | ortho-mcp · find_subcontract |
| 看法规节点 / 紧急度 | ortho-mcp · list_deadlines |
| "我有个产品要送检"（完整需求） | 检械通专家 |
| 问能力 / 安装 / 扩展 | 导航师直接答 |

## 三、安装引导（关键）

本工具箱的能力来自底层资产，**须先安装**：

1. **安装 medxpert-ortho-mcp 连接器**（开放平台连接器市场）
   - 上传 `ortho-mcp-connector.zip`，或在 mcp.json 配置该连接器。
   - 验证：会话重启后，工具列表出现 ortho-mcp 的 8 个工具。
2. **安装 检械通 专家（medical-device-testing-link）**（开放平台专家资产 / SkillHub）
   - 上传 `medical-device-testing-link.public.zip`。
3. **最后安装本工具箱（med-device-compliance-toolkit）** 作为门户前门。

> 顺序原则：先装底层连接器与专家，再装门户。缺任何一层，门户会提示先补齐。

## 四、扩展位（新增 MCP 资产）

要入住一个新 MCP 资产，做三步：

1. 在 `agents/med-device-compliance-toolkit.md` 的《工具箱索引》加一段（资产名 + 工具清单 + 何时用）。
2. 在本 SKILL.md 的《收录资产》《意图路由表》同步登记。
3. 如为新连接器，在 `manifest.json` 的 `dependencies.connectors` 补依赖名。

保持索引与实现一致即可，门户架构无需改动。

## 五、数据口径与合规（必读）

- ortho-mcp 的机构库（20 家）/ 标准库（43 条）/ 器械目录（18 类）/ 报价均为**示例数据**（随包 ortho-data.json，可替换），非真实资质。
- 凡输出候选榜或报价，必须注明「基于演示数据，正式委托前须向机构核验最新资质与报价」。
- 输出为对接参考方案，不替代法定检验；注册检验最终资质须用户自行核验；不得出具"保证通过"类承诺。
- 标准仅索引标准号 + 名称 + 官方来源，未内嵌受版权标准正文。
