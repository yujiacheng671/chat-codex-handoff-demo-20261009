# Chat 与 Codex 的最小任务交接

用 GitHub Issue 保存已确认的决定，用 PR 保存实现与验证证据。Chat 负责讨论与复核，Codex 负责实施。首次使用必须确认真实仓库、当前连接的读写权限与执行入口；本文本身不会安装自动化。

## 本次演示记录

本节记录 2026-10-09（Asia/Shanghai）编辑本文时的状态，不代表后续环节已经完成。

- 仓库：[chat-codex-handoff-demo-20261009](https://github.com/yujiacheng671/chat-codex-handoff-demo-20261009)，独立纯文档演示；基线为 `84736a95fd6781263a5181d8817adec9f60e4a57`。
- 任务：[Issue #1](https://github.com/yujiacheng671/chat-codex-handoff-demo-20261009/issues/1)。当前 GitHub 连接创建文件和 Issue 均返回 403，本 Issue 由 Codex 经用户已登录的 GitHub 网页创建。普通 Chat 创建 Issue 尚未验证成功。
- 当前 Codex 已通过 GitHub 只读工具读取 Issue #1，并依其要求在本地独立分支 `codex/handoff-demo` 实施，只新增任务模板与本文。这次执行由当前 Codex 会话分派启动，不能算作 Issue 自动触发。
- 草稿 PR 发布、真实远端提交检查及普通 Chat 对 PR 的独立复核均待完成；不得将本文或 Codex 自审作为已打通闭环的证据。后续结果应记录在 Issue/PR，检查须对应发布后的实际提交 SHA。
- 本次不配置 CI，文档验收采用差异格式和精确文件范围检查；没有 CI 不等于 CI 通过。保持 `main` 不变，不合并、不部署、不运行交易、不访问密钥。

## 一次任务的流程

1. Chat 把最终决定、修改范围、验收要求写成一个 Issue。先搜索同一任务是否已存在，存在则续用，避免重复创建。只记录必要上下文，不上传完整聊天记录、账户数据或密钥。普通 Chat 是否有创建 Issue 的工具，须在该会话中验证。
2. 使用已验证的执行入口启动 Codex。如果没有自动入口，在 Codex 发送一句“执行这个 Issue：〈链接〉，完成验证并开草稿 PR，不合并、不部署”。只传链接，无需复制讨论。创建 Issue、加标签或分配负责人均不等于已启动。
3. Codex 读取 Issue 和现有 AGENTS.md，检查工作区及相关自动化，创建独立分支。先复用现有检查，再做范围内最小改动；不修改交易策略、数据、配置或基础设施，除非该次任务明确要求并授权。首次演示只增加文档。
4. Codex 开草稿 PR，正文写“Refs #〈Issue编号〉”，附验收结果、实际运行的命令、退出结果、相关提交 SHA、未运行的检查及原因。把 PR 链接回填 Issue。不得自动合并或部署。
5. Chat 读取 Issue、PR 元数据、完整变更清单和 diff，再核对提交 SHA 对应的检查结果。输出“通过 / 需修改 / 证据不足”，引用具体文件或检查。PR 作者自述不等于已验证；没有 CI 也不等于 CI 通过。如果检查不到，明确标记。

## 日常一句话

讨论后：“把刚才确认的方案按已授权仓库的 Chat 任务模板建成 Issue，并通过已验证入口交给 Codex；只开草稿 PR，完成后把链接返回这里供我审阅。”

复核时：“读取这个 PR 及关联 Issue，按验收要求检查 diff、测试和未解决问题，给出是否可以由我合并的结论。”

一句话是请求格式，不是自动触发机制的保证。若普通 Chat 缺少写入或跨任务工具，必须报告缺失能力，不能声称已发送或已自动回传。此时最少手动交接是一次 Issue 链接启动 Codex，以及一次 PR 链接返回 Chat。

## 首次演示的验收

- 在真实授权仓库创建一个明确标注“演示，仅文档”的 Issue。
- Codex 从该 Issue 开始，在独立分支只新增交接文档或模板；检查现有工作流不会因推送或 PR 意外部署。
- 验证 diff 的文件范围和格式；记录真实的提交与检查结果。
- 创建草稿 PR，确认基础分支未改变；关联 Issue。
- 回到原普通 Chat 读取该 PR，完成一次独立复核。记录是哪一种会话、工具和提交 SHA 完成的，不能把 Codex 内自审记成普通 Chat 审阅。
- 保留 Issue、PR、执行任务、审阅结果链接；某步无法执行就保持“未验证”。

## 额度控制

先在 Chat 确定需求，再给 Codex 一个边界清楚的 Issue。把验收写清楚，减少返工；只读相关目录、diff 与必要日志。每个小任务通常一次实现和一次复核即可，不默认开启轮询或多代理。文档任务做静态检查，不运行完整交易程序。不要为连接流程额外安装常驻服务或申请 API key。

Work 和 Codex 共享额度。具体用量依套餐、模型、上下文与执行时长变化；不能承诺普通 Chat 的所有插件操作都不计入任何共享 credits，也不能承诺固定节省比例。

## 官方资料与触发边界

- [GitHub 集成](https://learn.chatgpt.com/docs/third-party/github)：PR 中的 `@codex review` 用于审阅；其他 PR 评论中的 Codex 请求可启动云端工作。这不是 Issue 自动执行的验证。
- [非交互执行](https://learn.chatgpt.com/docs/non-interactive-mode)：可用于已有本地 Codex 环境，但需要实际登录、仓库访问和运行条件。
- [Codex GitHub Action](https://learn.chatgpt.com/docs/github-action)：需要 API key；本最小方案不配置它。
- [额度说明](https://learn.chatgpt.com/docs/pricing)：Work 与 Codex 共用额度。

按 [GitHub 模板文档](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)，Issue 模板进入仓库默认分支后才可供新建 Issue 界面使用。在草稿 PR 阶段，可以由工具直接依据模板内容创建演示 Issue，无需提前合并。
