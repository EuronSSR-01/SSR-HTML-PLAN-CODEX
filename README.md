# SSR-HTML-PLAN-CODEX

在 Codex 中把开发方案做成可离线打开的交互式 HTML：逐层看方案、看界面草图、选择决策、添加批注，再把反馈复制回 Codex。

计划是一棵论点树：一级说用户能做什么（配界面草图或状态机），二级说怎么实现（配调用树、数据结构或代码），三级指到具体的 `文件:行`。需要你拍板的决策，就放在它影响的那个论点上。

这是基于 [Anthropic html-plan](https://github.com/anthropics/claude-plugins-community/tree/f60f0454df3045f724c43c6346ec80bdcc3472b2/html-plan) 的社区移植版，不是 Anthropic 或 OpenAI 官方产品。

## 安装

需要支持插件市场的 Codex CLI / Codex 桌面版、Git、Node.js 和浏览器。1.0.0 在 Windows、Codex CLI **0.159.2**、Node.js **24.13.0** 上验证过安装和使用；1.1.0 的打包检查和页面在 Windows、Node.js **24.15.0**、Microsoft Edge 上验证过，尚未在 Codex 里重新走一遍安装流程。这些是验证版本，不代表最低版本。macOS / Linux 尚未实际验证。插件无 npm 依赖、MCP 服务或专用 API Key；生成计划使用你当前 Codex 会话的模型。

在终端（Windows 可用 PowerShell）依次执行：

```powershell
codex plugin marketplace add EuronSSR-01/SSR-HTML-PLAN-CODEX
codex plugin add ssr-html-plan-codex@ssr-plugins
```

然后重启 Codex 桌面应用或打开新的 CLI 会话。CLI 与桌面需使用相同的 Codex 配置目录，才能看到相同安装结果。如果不通过 CLI 安装，在添加来源并重启后，也可以在桌面插件目录中选择 **SSR Plugins** 来源，找到 **SSR-HTML-PLAN-CODEX** 并点击安装。

查看安装状态：

```powershell
codex plugin list --marketplace ssr-plugins --json
```

本仓库为公开仓库，下载无需获得私人仓库授权。不单独提供 Release ZIP，分发方式为 GitHub 插件市场。

## 使用

在你的项目会话中输入：

```text
用 $ssr-html-plan-codex:ssr-html-plan-codex 为这个项目制作 UI 改造计划。
先阅读现有代码，给出布局、手机适配和需要我决定的问题。
生成交互式 HTML，先不要修改业务代码。
```

也可以直接说“用 SSR-HTML-PLAN-CODEX 做计划”，或从技能选择器中选择此技能；如果客户端显示带插件前缀的调用名，使用选择器给出的名字。在动手前让 Codex 出一份涉及多个文件的实施计划或技术方案时，它也可能自动选用这个技能。

1. Codex 读取相关代码，生成并打包 HTML，给出文件链接。
2. 用浏览器打开页面。折叠时只看到一级论点，它们就是整个改动的摘要；逐层展开，选择选项。内容旁边的 `+` 可添加批注，数据结构的 **编辑** 可直接修改。
3. 点击 **反馈 → 复制反馈**，把复制出的 Markdown 粘回 Codex。（英文计划的页面显示 **Respond → Copy response**。）
4. 确认方案后，明确告诉 Codex 是否开始实施。

默认选项只是建议。未打开的选项会标记为 `not opened; default kept`，不会被当作批准。页面不会自动发送消息或执行计划。

## 先看示例

克隆仓库后可以生成中文演示页。示例是一份虚构的“饭点小程序预约取餐”计划，三层齐全，包含界面草图、状态机、调用树、代码和 4 个决策：

```powershell
git clone https://github.com/EuronSSR-01/SSR-HTML-PLAN-CODEX.git
cd SSR-HTML-PLAN-CODEX
node plugins/ssr-html-plan-codex/skills/ssr-html-plan-codex/runtime/pack.mjs plugins/ssr-html-plan-codex/skills/ssr-html-plan-codex/examples/codex-plan-zh.html -o demo.packed.html
```

用浏览器打开 `demo.packed.html`。后续正式计划应在你自己的项目里生成。

## 更新和卸载

刷新市场并重新安装最新版本，然后开启新会话：

```powershell
codex plugin marketplace upgrade ssr-plugins
codex plugin add ssr-html-plan-codex@ssr-plugins
```

卸载插件：

```powershell
codex plugin remove ssr-html-plan-codex@ssr-plugins
```

如果不再使用本市场，再执行：

```powershell
codex plugin marketplace remove ssr-plugins
```

卸载插件不会删除你在项目里生成的计划。

## 常见问题

- **没有 `codex plugin` 命令：** 更新到支持插件市场的 Codex CLI，或使用支持该功能的桌面版。
- **安装了但找不到：** 打开新会话或重启应用，检查 CLI 与桌面的 `CODEX_HOME` 是否一致，以及所在工作区是否限制插件。
- **提示找不到 Node.js：** 安装 Node.js，或让 Codex 使用已有的本地 Node.js 运行时。本插件不会自动下载运行时。
- **GitHub 下载失败：** 检查本机访问 GitHub 的网络和 Git 代理配置。
- **已有同名独立 Skill：** 如出现重复条目，在备份后停用旧的独立版本，保留插件中的版本。安装器不会自动删除你的旧 Skill。
- **页面展示源码：** 下载或在本地浏览器中打开打包后的 `.html` 文件；不要只在 GitHub 源码页查看。
- **复制按钮被浏览器限制：** 从反馈弹窗手动选择并复制 Markdown。

## 文件与隐私

运行时不主动联网；选择和批注尽力保存在当前浏览器的 localStorage 中，受浏览器和文件路径限制。反馈以复制出来的文本为准。

生成的 HTML 可能嵌入项目代码。分享之前检查内容。插件里的示例是虚构数据。Lint 检查结构、长度和部分中文用词，不能代替代码测试或保证方案正确。

## 更新记录

**1.1.1**
- 把“文字简单、把事情说清楚”设为首要写作要求。必要时用两三句解释条件和结果，不为凑字数删掉关键意思。
- 长对话后先确认当前有效的需求，再重新组织文字；术语先解释，选项写清实际区别。
- 新增交付前的可读性检查，并把中文示例中的说明和选项改得更直白。

**1.1.0**
- SKILL.md 补回上游的完整方法：论点树对照表、页面骨架、11 条规则、步骤和反馈格式；新增具体的中文写作规范和替换表。英文计划的写法移到 `references/writing-en.md`。
- 中文示例重写为完整的三层计划。
- 中文页面（`lang="zh-CN"`）显示中文界面；状态机和流程图里的中文标签按实际宽度排版。
- 打包检查能统计中文：论点、问题、选项、句子和段落超长都会报警，长度按“字”显示；还会提示“进行”“应该”“相关”这类词和“被”字句。

**1.0.0**
- 首个 Codex 移植版。

## 许可和来源

采用 Apache-2.0，保留上游许可证及来源；详见 [LICENSE](LICENSE) 和 [NOTICE](NOTICE)。主要适配包括 Codex 调用与预览流程、中文计划与中文界面、中文长度和用词检查，以及面向 Codex 的反馈提示。

参考：[OpenAI 插件打包与市场说明](https://developers.openai.com/plugins/build/plugins)。
