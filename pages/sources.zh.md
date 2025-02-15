---
title: 应用源
description: 一些应用源的特定信息
---

# 应用源 {#app-sources}

添加、检查更新和安装应用的方式因来源和用户为该应用配置的设置而异。

以下选项适用于所有应用，无论其应用源如何：

- 仅跟踪：启用此选项后，您可以接收应用的更新通知，而无需尝试实际下载其 APK。这对于跟踪没有 APK 或无法通过 Obtainium 轻松提取 APK 的应用的更新非常有用。有些应用源只允许跟踪，例如 [ApkMirror](#apkmirror)。请注意，[版本检测](app_tracking.md/#version-detection)对任何添加为仅跟踪的应用都不起作用。
- 版本检测：请参阅[版本检测](app_tracking.md/#version-detection)部分。
- 通过正则表达式筛选 APK：当一个应用版本有多个 APK 时，系统会提示用户手动选择一个。这除了操作不方便之外，还意味着应用将不会在后台静默更新，即使在其它情况下可以这样做。该选项可让用户指定一个正则表达式，用于筛去不匹配的 APK（最好只有一个选项）。
- 尽可能按 CPU 架构筛选 APK：该选项将使 Obtainium 自动筛选掉任何与用户设备不兼容的 APK。筛选逻辑非常简单，是基于 APK 文件名，因此并不总是可靠的，在许多情况下，用户可能仍需要自己进行筛选。
- 应用名称：这允许用户为应用指定自己的名称，而不是使用 Obtainium 提取的名称。
- 禁用后台更新：该选项将防止应用在后台静默更新，即使后台更新已启用，并且该应用符合在后台更新的所有条件。
- 跳过更新通知：通过此选项，Obtainium 将避免通知用户此应用有可用更新或已在后台更新。

除此以外，每个应用还有额外的特定应用源选项。其中大多数选项不言自明，而且可能会经常更新，因此本 Wiki 不涉及这些选项。不过，有些应用源确实有更特殊的行为，需要更多解释说明，下文将对此进行介绍。

## 当前支持的应用源 {#currently-supported-app-sources}

- 开源——通用：
    - [GitHub](https://github.com/)
    - [GitLab](https://gitlab.com/)
    - [Forgejo](https://forgejo.org/)（[Codeberg](https://codeberg.org/)）
    - [F-Droid](https://f-droid.org/)
    - 第三方 F-Droid 仓库
    - [IzzyOnDroid](https://android.izzysoft.de/)
    - [SourceHut](https://git.sr.ht/)
- 其它——通用：
    - [APKPure](https://apkpure.net/)
    - [Aptoide](https://aptoide.com/)
    - [Uptodown](https://uptodown.com/)
    - [Huawei AppGallery](https://appgallery.huawei.com/)
    - [腾讯应用宝](https://sj.qq.com/)
    - Jenkins Jobs
    - [APKMirror](https://apkmirror.com/)（仅跟踪）
    - [RuStore](https://rustore.ru/)
- 特定应用：
    - [Telegram 应用](https://telegram.org)
    - [Neutron Code](https://neutroncode.com)
- 下载直链
- “HTML”（后备）：返回包含 APK 文件链接的 HTML 页面的任何其它链接

## GitHub {#github}

GitHub 对特定时间内的 API 请求数量设置了上限。由于 Obtainium 使用 GitHub API 抓取发布信息，因此如果你有几十个以上的来自 GitHub 源的应用，就可能会遇到“速率限制”错误。您可以添加个人访问令牌以解决此问题。

GitHub 还允许开发者托管其应用的多个版本。这通常是指同一应用的旧版本，但也可能包括预发布版本、变体等。——因此，Obtainium 提供了各种筛选器，让您可以浏览这些版本，并准确抓取您感兴趣的版本。

### 创建 GitHub 个人访问令牌 {#creating-a-github-personal-access-token}

1. 登录 [GitHub](https://github.com)。
2. 进入开发者设置中的 [Fine-grained tokens](https://github.com/settings/tokens?type=beta)。
3. 选择 **Generate new token**。
4. 给 Token 命名并设置有效期。
5. 滚动到底部，选择 **Generate token**。
6. 复制 Token 并将其粘贴到 Obtainium 设置中。请立即复制您的 Token，因为您将无法再次查看。

## GitLab {#gitlab}

GitLab 发行版中的 APK 有时会以非标准方式附加，导致 Obtainium 无法轻松获取。GitLab API 提供了更可靠的提取 APK 的方式，但没有 API 密钥就无法使用。虽然这对大多数 GitLab 仓库来说都不是问题，但您可以在 Obtainium 的设置中添加自己的个人访问令牌，以便在极端情况下更可靠地提取 APK。

与 GitHub 一样，GitLab 也允许开发者托管同一应用的旧版本，因此我们会根据情况提供其它选项。

### 创建 GitLab 个人访问令牌 {#creating-a-gitlab-personal-access-token}

1. 登录 [GitLab](https://gitlab.com)。
2. 进入设置中的[个人访问令牌](https://gitlab.com/-/user_settings/personal_access_tokens)。
3. 选择**添加新令牌**。
4. 给令牌命名并设置有效期。
5. 勾选 `read_api`。
6. 滚动到底部，选择**创建个人访问令牌**。
7. 复制令牌并将其粘贴到 Obtainium 设置中。请立即复制您的令牌，因为您将无法再次查看。

!!! info "何时需要这样做？"
    请参阅[该解释](https://github.com/ImranR98/Obtainium/issues/3#issuecomment-1234695412)，了解 GitLab 发行版中的非标准 APK 附件

## F-Droid 第三方仓库 {#f-droid-third-party-repo}

与大多数其它来源不同，F-Droid 仓库在同一链接下包含多个应用的信息。这意味着，除了版本库链接之外，您还必须单独提供所需的应用名称或应用包名。如果您不确定特定仓库中包含哪些应用，可以使用[导入/导出](ui_overview.md/#importexport-page)上的 “搜索来源”按钮来查找。

请注意，Obtainium 无法自动判断给定链接是否指向第三方 F-Droid 仓库。这意味着，默认情况下，向 Obtainium 添加第三方 F-Droid 仓库将导致错误使用 [HTML 源](#html)（Obtainium 在无法识别任何链接时使用的后备源）。您必须从“覆盖来源”下拉菜单中手动选择“F-Droid 第三方仓库”，才能解决这个问题。

## APKMirror {#apkmirror}

APKMirror 是一个“仅跟踪”源。这意味着，虽然您可以将 APKMirror 链接添加到 Obtainium 以获取更新通知，但无法下载和安装应用。这是因为 APKMirror 的维护者不允许这样做（参见 [issue #44](https://github.com/ImranR98/Obtainium/issues/44)）。

## HTML {#html}

“HTML”源是一个后备选项，可用于任何 Obtainium 不明确支持的应用源。由于其灵活性，它也是支持小众、不太流行的源，而不会使 Obtainium 变得臃肿的一种方式。

HTML 源的工作原理：

1. 首先向用户提供的源链接发送请求，并将响应解析为 HTML。然后在页面上查找链接。
2. 过滤掉某些链接。默认情况下，这是任何不以 `.apk` 结尾的链接，但您可以使用“自定义 APK 链接过滤器”来指定自己的过滤器。
3. 对剩余链接进行排序。这种排序是对整个链接进行字母数字排序，但你也可以选择只对链接的最后一段进行排序。最后一段通常是文件名，但如果在步骤 2 中使用了自己的过滤器，则可能不是。
4. 在所有剩余链接上应用另一个可选的用户定义过滤器。该过滤器与第 2 步中的过滤器的区别在于，它是所有应用源都有的更通用的过滤器——它继承自父类 `AppSource`（[应用源](#app-sources)中描述的 APK 过滤器选项）。在某些情况下使用它可能比在步骤 2 中使用一个更复杂的正则表达式更简单（示例请参见[该评论](https://github.com/ImranR98/Obtainium/issues/954#issuecomment-1745977857)）。与中间链接选项结合使用时也很有用。
5. 在剩余的链接中，它会选择第一个（如果启用了反向选项，则选择最后一个）。
6. 现在我们有了最终的 APK 链接，我们需要一个唯一的发布 ID 与之匹配，这样当 ID 发生变化时，我们就知道该应用有更新可用。对于其它源，唯一发布 ID 就是应用的版本，但对于 HTML 源，可能无法提取版本字符串。因此，默认情况下，将是链接的哈希值。
    - 但是，链接中通常会嵌入版本字符串。Obtainium 本身并不预知如何提取这些字符串（不同的网站会有不同的提取方法），因此用户可以选择指定一个正则表达式，应用于链接以提取版本——这就是“版本提取”的作用。
    - 但通常很难找到一个既能准确匹配版本，又能排除多余字符的正则表达式。为此，我们提供了“正则表达式匹配组”选项，让用户指定正则表达式中的哪个组作为版本。
    - 版本提取功能其实并无必要——使用链接哈希值更简单、更可靠。有些用户可能只是想要它，因为真实版本看起来更漂亮/更准确，而且它允许 Obtainium 在大多数情况下使用[版本检测](app_tracking.md/#version-detection)。

至于“中间链接”过滤器，如果使用该过滤器，HTML 源的工作原理如下（请参阅 [issue #820](https://github.com/ImranR98/Obtainium/issues/820)，了解在何种情况下该过滤器有用）：

1. 在 HTML 页面上查找链接。
2. 过滤掉与中间链接过滤器不匹配的任何链接。
3. 抓取剩余的第一个链接（此处没有反向选项），然后将该链接输入于前面所述的正常 HTML 源程序。

## 关于其它应用源的备注 {#notes-for-various-other-sources}

- HTML：请注意，HTML 源包括默认的请求标头，这些标头应适用于大多数网站。在某些情况下（例如 [SourceForge](https://sourceforge.net/)），您可能需要删除它们（也有可能需要自定义）。
- Codeberg：该源的附加选项几乎与 GitHub 相同。
- F-Droid：任何来自 F-Droid 的应用都可能使用不同的密钥[签名](https://developer.android.com/studio/publish/app-signing)，与其它源的相同应用不同。这意味着从 F-Droid 发布的特定应用更新到来自其它源（如 GitHub）的应用很可能会失败。
- 腾讯应用宝：来自该源的 APK 可能为纯 32 位（[armeabi-v7a](https://developer.android.com/ndk/guides/abis#v7a)）架构，无法安装在使用较新 Arm 架构 SoC 的某些设备上。
- 任何没有与之关联的特定服务器的源（如[第三方 F-Droid repos](#f-droid-third-party-repo)、Jenkins 和 SourceHut）都不会被 Obtainium 自动识别。您必须从“覆盖来源”下拉菜单中手动选择正确的源。
- 某些源（如 APKPure）可能提供 [XAPK 文件](https://apkpure.com/xapk.html)而非 APK 文件。Obtainium 的 XAPK 支持不完整，可能无法可靠运行。
