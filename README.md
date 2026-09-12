# [![](https://raw.githubusercontent.com/FFXIV-CombatReborn/RebornAssets/main/IconAssets/GBR_Icon.png)](https://github.com/MageritX/GatherBuddyReborn)

**GatherBuddyReborn — 国服版 (CN fork)**

![Github Latest Releases](https://img.shields.io/github/downloads/MageritX/GatherBuddyReborn/latest/total.svg?style=for-the-badge)
![Github All Releases](https://img.shields.io/github/downloads/MageritX/GatherBuddyReborn/total.svg?style=for-the-badge)
![Github License](https://img.shields.io/github/license/MageritX/GatherBuddyReborn.svg?label=License&style=for-the-badge)

GatherBuddyReborn is a community-made fork of the original GatherBuddy plugin for Final Fantasy XIV. This tool is designed to enhance your gameplay experience by assisting with all things gathering, now with automated routes via vnavmesh.

本仓库是 GatherBuddyReborn 的 **国服（简体中文客户端）适配分支**，基于 [AtmoOmen/GatherBuddyReborn](https://github.com/AtmoOmen/GatherBuddyReborn) 的国服 fork 继续维护，并持续合并上游 [FFXIV-CombatReborn/GatherBuddyReborn](https://github.com/FFXIV-CombatReborn/GatherBuddyReborn) 的更新。

国服版与国际版的区别：

- 支持国服客户端的 `ClientLanguage.ChineseSimplified` —— 国际版插件在国服客户端上会直接加载失败（`MultiString.Name` 抛 `ArgumentException`）
- 枚举成员、界面、状态栏与日志文本全部中文化
- 跟随上游合并新功能（当前已并入上游 39 个提交，开源发布版本 **7.5.0.8**）

## Features

- **AutoGather**: Automated pathing for gathering up to 10 full stacks (999 each) of a resource.
- **Resource Queueing**: Create a list of resources you want and GBR will gather up to 10 stacks of each!
- **Full BTN/MIN Automation**: GBR can find any BTN/MIN item in the world and gather it for you fully automatically, no user input required beyond initial setup

**NOTE**: vnavmesh plugin is *required* for full automation. Please see the links section of this README for more information on vnavmesh.

## Installing / 安装

### 国服版（本仓库，国服玩家请用这个）

1. 游戏内输入 `/xlsettings` → **实验性 / Experimental** 选项卡 → 找到 **自定义插件仓库 / Custom Plugin Repositories**
2. 在第一个空输入框粘贴下面的地址（国内建议用 jsDelivr 线路），点右侧 `+` 号，确认勾选框已勾上，然后点右下角保存：

```
https://cdn.jsdelivr.net/gh/MageritX/GatherBuddyReborn@main/pluginmaster.json
```

备用地址（raw.githubusercontent）：

```
https://raw.githubusercontent.com/MageritX/GatherBuddyReborn/main/pluginmaster.json
```

3. 输入 `/xlplugins` → 搜索 **GatherBuddyReborn** → 安装
4. 自动采集还需要安装并启用 [vnavmesh](https://github.com/awgil/ffxiv_navmesh)

> ⚠️ 本插件的内部名（InternalName）与官方仓库的 GatherBuddyReborn 相同。如果你已经添加了 `FFXIV-CombatReborn/CombatRebornRepo`，请把本仓库放在它**前面**，或移除其中 GatherBuddyReborn 这一项。否则卫月会优先使用官方（国际）版，在国服客户端上无法加载。

### 国际服版（上游）

- Enter `/xlsettings` in the chat window and go to the Experimental tab in the opening window.
- **Skip below the DevPlugins section to the Custom Plugin Repositories section.**
- Copy and paste the repo link into the first free text input field:

```
https://raw.githubusercontent.com/FFXIV-CombatReborn/CombatRebornRepo/main/pluginmaster.json
```

- Click on the `+` button and make sure the checkmark beside the new field is set afterwards.
- **Click on the Save-icon in the bottom right.**

Following these steps, you should be able to see all contained plugins in the Available Plugins tab in the Dalamud Plugin Installer.
No Plugins will be installed, you have just made them available. You can now select which of these plugins you actually want to install.

## Building / 自行编译

```
git clone --recurse-submodules https://github.com/MageritX/GatherBuddyReborn.git
cd GatherBuddyReborn
dotnet build -c Release GatherBuddy/GatherBuddy.csproj
```

需要 [.NET 10 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/10.0) 以及一份 Dalamud 开发环境（[XIVLauncher](https://github.com/goatcorp/FFXIVQuickLauncher)，国服使用卫月 / XIVLauncher CN）。

国服版**必须**使用国服 Dalamud：`GatherBuddy.GameData`、`GatherBuddy.DataImport`、`GatherBuddy.Levenshtein` 通过 `Dalamud.CN.NET.Sdk` 从 `%APPDATA%\XIVLauncherCN\addon\Hooks\dev` 解析引用，官方 goatcorp 分发的 Dalamud 缺少 `ClientLanguage.ChineseSimplified`，会报 `error CS0117`。也可以用 `DALAMUD_HOME` 环境变量指向该目录。

## Releasing / 发版（维护者）

1. 修改 `GatherBuddy/GatherBuddy.csproj` 里的 `<Version>`，版本号依次递增（例如 `7.5.0.8` → `7.5.0.9`）
2. 推送到 `main`
3. 打同名 tag 并推送：`git tag -a 7.5.0.9 -m 7.5.0.9 && git push origin 7.5.0.9`

CI（`.github/workflows/publish.yaml`）会自动完成：构建 → 创建 / 更新 release（资产 `GatherbuddyReborn.zip`）→ 更新本仓库的 `pluginmaster.json` → 刷新 jsDelivr 缓存。

> 工作流中 `cn-dalamud-dev-*` 预发布资产是 CI 编译所需的国服 Dalamud 参考程序集，**请勿删除**，否则发布与 PR 测试构建都会失败。

## Want to contribute?

- Create a fork
- Make your changes
- Test the changes
- Create a PR and point it to main

## Links

[vnavmesh](https://github.com/awgil/ffxiv_navmesh) Required for automated navigation

[FFXIV-CombatReborn/GatherBuddyReborn](https://github.com/FFXIV-CombatReborn/GatherBuddyReborn) 上游国际版仓库

[AtmoOmen/GatherBuddyReborn](https://github.com/AtmoOmen/GatherBuddyReborn) 本分支所基于的国服 fork

## Attribution and Acknowledgements

GatherBuddyReborn and its various functions relies heavily on the original foundations of various individuals whom without their prior works GatherBuddyReborn would not be the utility it is today and in the future. These attributions are NOT implied as endorsements of GatherBuddyReborn. In alphabetical order:

    - All of the contributors to Dalamud and FFXIVLauncher
    - [Artisan](https://github.com/PunishXIV/Artisan): Taurenkey, pksage, Limiana, et al.
    - [GatherBuddy](https://github.com/Ottermandias/GatherBuddy): Ottermandias, et al.
    - [vnavmesh](https://github.com/awgil/ffxiv_navmesh): awgil, xanderscore, et al.

国服适配相关的致谢：

    - [AtmoOmen/GatherBuddyReborn](https://github.com/AtmoOmen/GatherBuddyReborn): AtmoOmen — 国服客户端适配与中文化，本分支的前身
    - 本仓库由 MageritX 维护：跟随上游合并更新、国服编译与 CI 发版
