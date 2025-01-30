---
title: 如何跟踪应用
description: 如何在 Obtainium 中跟踪应用
---

# 如何跟踪应用 {#how-apps-are-tracked}

### 基础 {#basic}

向 Obtainium 添加应用链接时，必须选择一个[应用源](sources.md)。应用源定义了如何从您输入的链接中提取应用信息和 APK 文件。大多数情况下，Obtainium 会自动选择要使用的应用源，如果无法选择，则会显示“覆盖来源”下拉菜单。

至少，应用源必须为其应用提供以下数据：

- 应用版本（或“伪版本”——为应用的每个新版本而改变的标识符）
- 至少一个与所提供版本相对应的 APK 下载链接

应用源还可提供其它信息——这些信息可提供额外功能或用户界面优势。例如：

- 应用作者
- 应用包名
- 最新版本的发布日期
- 应用旧版本或其它变体信息

在理想的情况下，每个应用源都能以简单明了的方式提供所需的全部信息——每个给定的链接只提供一个应用，并以标准格式提供所需的全部信息。但实际情况往往并非如此——即使是同一个应用源，也有许多不同的应用发布处理方式，因此不可能有一套固定的步骤来处理所有应用。因此，在添加应用时，您会看到各种附加选项，这些选项可用于修改提取应用信息的方式。虽然默认值适用于大多数应用，但您可能需要了解这些选项以处理极端情况，更多信息请参阅下面的[应用源](sources.md)部分。

注意：Obtainium 中的许多筛选器设置（包括许多特定于应用源的可选筛选器）都使用了[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_expressions)——你应该熟悉这些。

### 版本检测 {#version-detection}

Obtainium 在跟踪当前已安装的应用时，会从 Android 中获取应用版本，并将其与源提供的版本字符串进行比较。然后，它将两者进行比较，以确定是否有可用的更新，或应用的安装状态是否已发生变化。只有在两个版本格式相同的情况下，才能进行比较，但情况并非总是如此。例如，您可能会遇到以下任何一种情况：

1. 来自 GitHub 源的 [Obtainium](https://github.com/ImranR98/Obtainium/releases/tag/v0.14.21-beta)：

    - **来自 Android 本地的应用版本号：** `0.14.21`
    - **来自应用源的版本号：** `v0.14.21-beta` 

2. 来自 SourceHut 源的 [Cheogram](https://git.singpolyma.net/cheogram-android/refs/2.12.8-2)：

    - **来自 Android 本地的应用版本号：** `2.12.8-2+free`
    - **来自应用源的版本号：** `2.12.8-2`

3. 来自 Tor 官网的 [Tor](https://www.torproject.org/download/)：

    - **来自 Android 本地的应用版本号：** `102.2.1-Release (12.5.6)`
    - **来自应用源的版本号：** 无（该 HTML 源未提供版本字符串，因此使用链接哈希值作为“伪版本”）

4. 来自 GitHub 源的 [Quotable](https://github.com/Lijukay/Qwotable/releases/tag/v10)：

    - **来自 Android 本地的应用版本号：** `1`
    - **来自应用源的版本号：** `v10`

Obtainium 会存储一个“标准”格式列表，用于进行比较（如 `x.y.z` 或 `x.y`）。如果比较的两个版本符合相同的格式，则将进行比较。否则，将禁用该应用的版本检测。在某些情况下，Obtainium 会从源字符串中删除多余的部分，这样处理将产生一个标准版本号（例如从 Obtainium 的 `v0.14.21-beta` 中删除 `v` 和 `-beta`），然后即可进行比较。我们从不试图从操作系统提供的“真实”版本中剥离部分内容。

[该代码片段](https://github.com/ImranR98/Obtainium/blob/main/lib/providers/apps_provider.dart#L64)定义了各种“标准”格式的生成方式。

我们随时都可以扩展这段代码，添加对更多格式的支持，但这需要慎重考虑。例如，如果 Android 本地某个已安装应用的版本是“1.2”，但应用源显示该应用的最新可用版本是“1.2-4”，我们是否应该去掉 `-4` 并说两者是相同的（意味着没有可用的更新）？在某些情况下（即 `-4` 实际上并不表示应用本身发生了变化）这样做可能没有问题，但在其它情况下就不行。因此，支持这种特定情况并不是一个好主意。

关闭版本检测通常不会对日常使用产生重大影响。如果禁用了某个应用的版本检测，您可能偶尔会遇到本地应用真实版本与 Obtainium 界面中显示的版本不一致的情况。这种情况只会在两种情况下发生：

1. 如果本地应用的版本因 Obtainium 之外的操作而发生变化（例如，如果它被 Google Play 更新）。
2. 如果 Obtainium 尝试在后台[静默更新](#background-updates)应用失败

在这种情况下，Obtainium 无法检测到本地应用的真实版本已更改，因此无法相应更新其内部记录——您需要手动纠正不一致。

另请参阅：[Obtainium issue #946 评论](https://github.com/ImranR98/Obtainium/issues/946#issuecomment-1741745587)

## 后台更新 {#background-updates}

Obtainium 会定期在后台检查应用更新。您可以在设置页面上控制这些更新任务的频率。

后台更新检查任务完成后，任何可用的更新都会被分为两类：

1. 可在后台应用的更新
2. 无法在后台应用的更新

要在后台自动安装更新（又称静默更新），必须满足某些条件：

- 操作系统必须是 Android 12 或更高版本
- 安装的应用必须是[较新的 Android API 版本](https://developer.android.com/reference/android/content/pm/PackageInstaller.SessionParams#setRequireUserAction(int))
- 当前安装的应用版本必须由 Obtainium 安装
- 您必须在 Obtainium 中启用后台更新（无论是普遍的，还是特别针对此应用的——这是默认设置）
- 如果有多个 APK 可用于更新，则必须配置该应用的附加选项，以便 Obtainium 能够将这些 APK 筛选为一个 APK

在可能的情况下，下载并安装每个可用的更新，然后通知用户更新可用或已在后台安装。

请注意，由于技术限制，后台更新只能以异步、尽力的方式安装。因此，如果后台更新安装失败，您将不会收到错误通知。
