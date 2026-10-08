# 执行顺序与注意事项

先按 SKILL.md 确定用户指定的笔记根目录 NOTE_ROOT。本文中的原文、源文档和资源均指该目录下的当前文件；历史版本、软件列表及配置偏好与当前笔记冲突时，以当前笔记为准。

## 1. 准备

确认 Windows 版本/架构、当前用户、管理员权限、目标磁盘、代理可达性、已有安装和待重启状态。先读取源文档当前阶段再执行。下载用官方发布页、已核对的 winget/Scoop 来源；下载包有官方哈希时校验，Windows 安装器能验证签名时核对发布者。

“开始”中的分区、重装、删除旧账号、移动桌面/文档/下载目录由用户手动处理。不要因其出现在文档而自行执行。代理客户端、浏览器同步、账号登录、云盘资料及付费激活属于人工依赖，可先完成不依赖这些内容的任务。代理 1130 是本机偏好，先测试，不可把不存在的代理写入所有工具。

以非管理员 PowerShell 安装用户级 Scoop。仅需提权的安装或设置单独提权。任何配置写入先读取并保留备份；环境变量增量合并，避免重复 PATH 和覆盖现有用户设置。

## 2. Scoop → Git → PowerShell → Terminal

1. 按 Scoop“基本安装”设置当前用户 RemoteSigned、安装 Scoop；必要时先下载官方安装脚本并通过已验证的代理执行。
2. 设置 Scoop 代理，安装 Git，配置 Git 代理，然后添加 extras，安装 `pwsh windows-terminal`。后续再添加 java、versions、nonportable、dorado、lemon、nirsoft-alternative，更新索引。先核对仓库是否已存在，添加失败不能视为成功。
3. Git 基本配置：个人身份、`core.editor="code --wait"`、`core.quotepath=false`、`core.autocrlf=input`。SSH 密钥先检查已有文件；私钥不导出到技能或云盘，添加 GitHub 公钥等账号操作交给用户。
4. 按 Git 文档安装 zsh 和 powerlevel10k。这里的 zsh 是覆盖 Git 安装目录式安装，不能擅自换为 WSL 方案。更新或清理 Git 时需从 PowerShell 操作，避免占用的 Bash/zsh 进程；不要强制终止用户活跃会话。Git 更新可能需要重新覆盖安装 zsh。
5. 分别在 Windows PowerShell 5.1 与 PowerShell 7 中发现 `$PROFILE`，合并 Scoop、代理和 shell 快捷命令。用函数转发参数，不把含参数命令写成普通别名。先查内置别名冲突，不让文档中的“无冲突”描述代替实际检查。
6. 备份 Terminal 的实际 settings.json，保留既有 GUID 和无关配置。Bash 为默认，Bash 和 PowerShell 起始目录都为 `D:\project\self`；磁盘存在而目录缺失时可创建。字体 MesloLGS NF、字号 10、启动大小 120×25、选中复制，Bash 外观按原文设置。不要创建重复的 PowerShell 7 入口。
7. 字体下载后列出四个字体文件路径，让用户打开并点击“安装”。本次经验显示仅复制字体和写注册表不能保证不弹窗。Terminal 右键菜单明确由用户手动处理，不重试自动注册。只有 Scoop 版已实际验证且旧版移除在当前范围内时才考虑卸载商店版，不以新安装成功作为删除依据。
8. VS Code 默认终端设为 Git Bash；安装 aria2 并配置原文参数。仅遇到 aria2 问题时关闭它。缓存损坏只清理对应包，不跳过哈希校验。

## 3. 常用软件与设置

按优先事项“软件安装”逐项处理，列表只是渠道分类，不把软件排在下面误认为可选。完整软件名称、选项和资源以 NOTE_ROOT 下的当前源文档为准。

- winget 先查询准确包标识、发布者和版本，不凭显示名直接选首个结果；官网/GitHub 项查最新稳定发布及所需完整包，不下载源码当安装包。
- UWP：按目标机实际包身份配置需要的网络回环，微软商店受代理影响时先诊断；不全局开放所有应用。Feem 按需要配置应用级防火墙规则。
- NVIDIA App 用 NVIDIA 官网安装器；NVIDIA 控制面板用 Microsoft Store 页面。仅安装 App 不等于授权升级显卡驱动。原文信息浮窗设置需另外核验。
- AutoHotkey 脚本来自 `NOTE_ROOT/系统/win/software/resources/start.ahk`；核对脚本与已装 AHK 主版本兼容，再放入实际 Startup 目录。
- TrafficMonitor 必须先应用自动背景色和深浅主题适配，再启用透明色，按原文顺序执行。
- Typora 配置直接读取 NOTE_ROOT 下的 `系统/general tools/typora.md`，不把“配置在云盘”当作阻塞。先关闭并确认保存用户文档再改配置；插件使用官方仓库、核对实际安装目录。配置文件验证与插件界面验证分开记录，软件升级后可能需重新运行插件补丁。
- Lenovo Legion Toolkit 仅适用于兼容联想机型。独显直连及冲突服务处理需先检查当前硬件和软件状态，不能对所有新电脑执行。
- 欧路词典的软件可安装；本次用户选择跳过词典设置。下次默认保留这个偏好，但用户新指示优先；不要求先提供词典文件才能安装其他软件。
- UACWhitelistTool 没有目标名单时不添加白名单；游戏加加没有进程名单时不猜排除项。Wallpaper Engine 未启用时不强制套用其条件配色。
- `.reg`、JSON、TOML、XML 写入前核对格式和实际路径，保留无关值。原文 mpv.reg 含旧机路径时必须替换。

以下是旧机遗留待核验项，不是新机必然失败项：X-Mouse 的 Typora 鼠标 4/5 键；游戏加加 Ctrl+F5 与注入排除名单；WPS 附加功能关闭；联想冲突服务；Typora 新建 Markdown 菜单；mpv 浏览器端播放；多显示器任务栏实际行为。新机在范围内可执行一次并验证；失败后记录实际原因，不沿用旧机“已完成”结论。

## 4. 开发环境

基础工具按 Scoop 文档安装；`si` 等是 Bash 别名，自动化 PowerShell 中使用完整 `scoop install`。基础列表中的 VisualVM 属可选配置项，本技能默认跳过其安装与配置，用户要求完整基础列表时再包括。保持用户明确指定的版本；对 Java 25、Python 3.12 等偏好不擅自替换为“最新大版本”。

### Java

- 默认 JDK 按源文档，JDK 8 为历史兼容环境。旧机使用 Oracle 8u202；下载验证签名后若安装器失败，可核对安装器结构提取 JDK、执行 unpack200 并验证 java/javac，再设置 JAVA8_HOME；保留默认 JAVA_HOME。不要凭旧版本经验硬编码 PE 内部资源路径。
- Maven：合并 `resources/settings.xml` 至实际用户 `~/.m2/settings.xml`，使用阿里镜像；已有凭据和服务器配置保留。
- Gradle：合并 `resources/gradle.properties` 的代理等配置，现代 JDK 删除废弃 `-XX:MaxPermSize=512m` 参数；旧机 Gradle 9.8/JDK 25 已验证该调整。代理端口随本机实际配置。
- IDEA 安装后设 Git Bash shell 与选中复制。2026.2 使用 `terminal-local.xml` 的 TerminalLocalOptions/shellPath 和 `terminal.xml` 的 TerminalOptionsProvider/myCopyOnSelection；这是历史格式线索，写入前核对目标版本。账号同步由用户完成。

### Python / Conda

- Python 3.12 为默认；pip 阿里镜像并升级。只有遇到已知 pip 升级文件问题时采用先装 requests 再升级的办法。
- Poetry 可能安装另一 Python，Anaconda 也带 Python；不为了默认 3.12 删除它们。核对新终端 `Get-Command python` 和 `python -m pip --version`，不能只看 scoop list 或 scoop reset 成功提示。
- 验证 uv、Poetry；不创建原文示例业务项目，不安装示例 torch、MinerU 或 cuDNN。
- `conda init powershell`，关闭自动激活 base，在两套 PowerShell profile 中合并 Conda 快捷命令。确认 conda 是带激活能力的 shell 函数；新会话 base 未自动激活。

### JS / TS

- NVM 安装并选择当前 LTS，再在该 Node 中全局安装 pnpm、Yarn、Bun、NestJS CLI；配置 npm/pnpm/Yarn 的 HTTP 与 HTTPS 代理。删除代理、清缓存属于使用说明，不安装后立即执行。
- npm registry 镜像在原文已划除，保留官方源。NVM 官方下载发生可重现超时时可核验官方 LTS 后改用文档记录的 npmmirror Node 镜像，并记录变更；Node 二进制镜像与 npm registry 是两项配置。
- NVM v2 的 Scoop 安装可能不能自动刷新入口：安装全局包后执行 `nvm reshim`，再验证 pnpm/yarn/bun/nest；不要全局关闭信任校验。npm 若拦截刚安装包的必要脚本，只对核实过的具体包允许一次安装脚本，不设置全局无条件放行。
- Codex 等宿主自带 Node 可能在进程 PATH 前面，验证应使用目标用户新终端和 NVM 实际入口。
- Vue/Electron 项目创建与业务依赖示例跳过。Scoop 文档中另一个章节的 AI CLI、容器等不自动并入“具体语言配置”。

### Go / Android

- Go：`GOPROXY=https://goproxy.cn,direct`，安装文档两个 protobuf 生成器，确保实际 GOPATH/bin 可见。原文 protoc-gen-go 使用旧 github 模块；如需迁移必须说明兼容性，不能静默改变。BloomRPC 可用官方完整安装器。
- Android：安装 Android Studio、官方 SDK command-line tools、platform-tools、稳定平台和相配 Build Tools。核验官方哈希和 SDK 许可要求。设置 ANDROID_HOME（兼容时同步 ANDROID_SDK_ROOT）、platform-tools/CLI PATH；不额外下载模拟器镜像，不对手机执行原文冻结、卸载命令。
- CLI 安装成功与 Android Studio 首次启动完成分开记录。

## 5. 四个游戏助手（用户选择时）

完整开发环境的后续顺序：Node 就绪后按 Scoop 的独立章节安装用户要求的 Codex、OpenCode、MiMo CLI，账号或模型令牌由用户提供；相关 OpenAI 产品操作使用目标环境可用的官方文档或对应技能。Docker Desktop 放在其他安装完成后，因为可能启用 WSL 并需要重启；记录重启要求，让用户选择重启时间。NOTE_ROOT 下的容器文档中的 Kubernetes、Istio、kubeconfig 合并和部署不是安装 Docker 的隐含动作，仅在用户明确选择本地集群配置时执行，并先核对当前 context，不能对已有远程集群直接套用 demo 命令。

从优先事项所列官方 GitHub 仓库查询最新稳定发布，选 Windows 实际架构的便携完整包：

| 项目 | 包选择 | 目标子目录 |
| --- | --- | --- |
| moesnow/March7thAssistant | full.7z 或 full.zip，不用 update 包 | March7thAssistant_full |
| OneDragon-Anything/ZenlessZoneZero-OneDragon | WithRuntime-Full（含运行时与模型）；核对当期发布说明 | ZenlessZoneZero-OneDragon |
| miaojiuqing/Maa_bbb | win-x86_64 或对应机器架构 ZIP | Maa_bbb |
| babalae/better-genshin-impact | BetterGI 便携 7z，不用 Install.exe | BetterGI |

默认根目录 `E:\miHoYo\maa`。先检查目录内容，已有配置不可覆盖；核对压缩包自带根目录避免多套一层。校验哈希和解压退出码、确认启动文件。下载解压请求不包含启动游戏、自动化运行或配置账号。

## 6. 验证、恢复与报告

- 命令行：用新用户环境验证实际可执行路径和版本；验证代理值、Conda 不自动激活、两套 profile 无加载错误。Gradle 可在临时目录执行 help，Go 可生成临时 proto 文件；验证资源留在临时目录，不创建用户业务项目。
- GUI：有可用 UI 工具时检查设置生效；仅检查配置文件的项目标为“配置已写入，界面未验证”。菜单注册存在不等于菜单能用。
- 旧机曾有沙箱权限导致的 Java 配置读取、Conda 输出重定向和 winget 调用错误。区分沙箱限制与真实主机故障，按当前权限机制申请所需权限，不据此破坏本机配置。审批拒绝不绕过。
- 修改 Markdown 保持 UTF-8 与原有换行风格，避免 LF/CRLF 产生无正文差异的修改标记；只规范本次触及内容，不覆盖用户其他改动。
- 安装中断时根据当次记录继续，重新检查未完成进程/安装结果，避免重复下载、重新创建配置和重复提问。历史退出码不代替当前状态。
