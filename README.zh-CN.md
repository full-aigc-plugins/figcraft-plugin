# FigCraft Use

## Installable editor development candidate

`0.1.0-dev.20261017.1` is distributed through the Full AIGC plugin marketplace as a development prerelease. Node.js 24 is required. Git installations use `ui/bootstrap.mjs` to download and verify the pinned editor archive on first start; complete release ZIPs also include that archive unpacked for offline startup. No Rust build or npm installation is required. Startup diagnostics use stderr; stdio remains MCP-only. The editor shares its session with Agent commands. Full creative quality and all-host embedded UI acceptance are still incomplete. Existing dated validation below describes its original version.


独立插件，包含官方图标、stdio MCP、MCP Apps 面板和 7 个界面设计场景技能。当前为本地未发布候选；没有修改全局插件设置。

编辑器基于 FigCraft v0.6.0 的固定源码加入自动化与工作区文件桥接，参考 Craft craft-runtime，保留其 Apache-2.0 许可。`ui/source.lock.json` 记录来源提交；`ui/editor.lock.json` 记录内置制品摘要。它是我们构建的增强版，不是官方原版 Web ZIP。

通过 `open_editor` 在支持 MCP Apps 的宿主显示；宿主未渲染时，用 `open_browser_editor` 返回的 URL 在宿主内置浏览器打开。Codex Desktop 可使用 `open_in_codex`。不支持 Apps 或内置浏览器的 MCP 客户端无法靠服务器配置获得内部页面。

## 使用

运行环境：Node.js 24。已构建候选的入口是 `node ui/dist/adapter.mjs`，使用 stdio。工作区通过 `CRAFT_WORKSPACE_ROOT` 指定。`--serve` 用于单独展示界面，自动化必须连接同一个 MCP 实例。

- `open_editor` / `open_browser_editor`：打开界面。
- `create_node`、`set_properties`、`run_command`：编辑可见文档。
- `inspect_document`、`screenshot`：检查结构与画面。
- `save_file`、`open_file`、`export`：工作区工程保存、重开与导出。

首次打开尝试下载本插件最新兼容增强发行包；未发布、下载失败或接口不兼容时使用内置版本。`CRAFT_EDITOR_UPDATE=off` 可明确选择内置资源。

## 宿主配置

使用完整插件市场包安装。Codex 入口为 `.codex-plugin/plugin.json` 和 `.codex-plugin/mcp.json`；Claude Code 入口为 `.claude-plugin/plugin.json` 和根 `.mcp.json`。标准宿主读取 `plugin.json` 和 `mcp.json`。安装路径由宿主解析，不再推荐逐项绝对路径配置。

## 验证

源码增强构建已在本机通过创建 frame/文字、保存重开、PNG 导出、页面刷新与断开回归。`ui/tests/editor-smoke.mjs` 是可重复的实际 stdio + Chromium 测试。它不等于每个目标宿主均已安装验收。

构建方法见 [ui/README.md](ui/README.md)；源码技能在独立 `figcraft-skills` 仓维护，本地副本由 `scenario-candidates.json` 校验。

源码增强候选采用 `ui/source.lock.json` 与 `ui/build-source.py`；兼容更新查询本插件自有 GitHub Releases，失败回退内置，原版 Web 不替换增强自动化运行时。当前会话保留；宿主安装验收另行记录。

## 界面场景操作手册

新增8条界面设计流程，见 [figcraft-scenario-playbooks](skills/figcraft-scenario-playbooks/SKILL.md)。包含实际返回ID绑定、父子结构、自动布局和独立CLI执行脚本；宿主同步显示验收单独记录。

## main新增能力候选

新增[自动保存与协作成员控制指导](skills/figcraft-scenario-playbooks/references/main-workflows.md)，包括2个新方法和5处契约变化。仅核对固定main真实参数；新增业务、浏览器托管及协作服务器验收未完成。
