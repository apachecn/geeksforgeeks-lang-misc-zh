# Lint 及其在安卓工作室的使用

> 原文:[https://www . geesforgeks . org/lint-and-it-in-Android-studio/](https://www.geeksforgeeks.org/lint-and-its-usage-in-android-studio/)

作为安卓开发者，我们都利用安卓工作室来创建我们的应用。有许多可供选择的编辑器可以用于安卓应用程序开发，但吸引我们来到安卓工作室的是它为安卓开发者提供的帮助。这种帮助可能采取自动建议的形式，或者显示代码中的错误(在我们项目中存在的所有文件中)。所以，在本文中，我们将看看 **Lint** ，这是 Android Studio 最伟大的方面之一，帮助我们增强了编写无错代码的能力。

**本文将涵盖以下主题:**

1.  皮棉到底是什么？
2.  棉绒形态
3.  使用基线辅助除绒

### 1.皮棉到底是什么？

Lint 是 Android Studio 提供的代码扫描工具，可以识别、建议和纠正项目中不正确或危险的代码。

> **GeekTip #1** : Lint 的功能类似于成熟的堆栈分析框架。

自从我们第一次开始使用安卓工作室以来，我们都一直在使用 Lint，因为它在每个项目中都标配了对 Lint 的支持。Lint 会通知您代码中发现的任何错误，以及一些建议和警告级别。您可以使用该建议对代码进行更改。Lint 最大的特点是你可以以任何你认为合适的方式使用它。如果您在项目中提供了某种类型的错误，Lint 只会显示这种类型的错误。皮棉在自然界中适应性很强。当您创建项目时，安卓工作室会自动执行检查过程，但是您也可以手动或使用 Lint 从命令行检查您的代码。

**除绒可以分为三个步骤:**

1.  **制作 lint.xml 文件:**在 lint.xml 文件中，您可以修改 lint 检查。您可以在此文件中写入想要包含的检查，而忽略不想包含的检查。例如，如果您希望检查未使用的变量，但不检查命名问题，您可以在 lint.xml 文件中这样做。除此之外，您可以手动配置 Lint 检查。在本文的下一部分，我们将了解如何执行手动 lint 检查。
2.  **Lint 检查:**下一步是选择将要进行 Lint 检查的源文件。它可能是您项目的. java 文件。kt 文件或任何 XML 文件。
3.  **Lint Remover:**最后，Lint 工具会检查源代码和 lint.xml 文件中的结构代码问题，如果有，还会提出代码更改建议。建议我们在发布程序之前应用 lint 建议。

**什么时候应该使用棉绒？**

如果您希望在游戏商店或任何其他应用商店发布您的应用，它必须是无错误的。为此，您必须在应用程序上进行大量的手动测试。

> **极客提示#2** :但是，如果您希望消除部分手动测试，您可以将 Lint 合并到您的项目中。

如果您检查代码中的每个文件是否有错误，Lint 将检测到问题并提出解决方案。错误或警告可以是以下类型:

1.  未被利用的变量
2.  不合理的例外
3.  项目不需要的导入，以及更多

*所以，在发布你的应用之前，使用 Lint 彻底检查你的代码。*

**您也可以在项目的多个层设置 lint 检查:**

1.  全面(整个项目)
2.  项目模块
3.  生产模块测试模块
4.  应该打开文件
5.  版本控制系统(VCS)在类层次结构中起作用

### 2.棉绒配置

要利用 lint 或仅在项目中运行检查，请将 Lint 检查添加到 lint.xml 文件中，或者使用 Android Studio 在项目中手动选择 Lint 要配置的问题列表。

**配置 lint 文件:**

在 lint.xml 文件中添加要配置的问题列表，以便在应用程序中定义手动检查。如果你创建了一个新的 lint.xml 文件，把它放在你的 Android 项目的根目录下。

**这里有一个 lint.xml 文件的例子:**

```kt
<?xml version="1.0" encoding="UTF-8"?>
<lint>
    <issue id="GeeksIconMissing" severity="error" />
    <issue id="OldDimens">
        <ignore path="res/layout/merger.xml" />
        <ignore path="res/layout-xlarge/merger.xml" />
    </issue>
    <issue id="HellOWorld">
        <ignore path="res/layout/main.xml" />
    </issue>
    <issue id="someText" severity="ignore" />
</lint>
```

**手动配置棉绒:**

默认情况下，lint 会检查一些问题，但不是所有问题。这是没有做到的，因为运行 lint 可能检查的所有问题检查将会降低安卓工作室的速度。因此，默认情况下，安卓工作室只使用有限数量的棉绒检查。但是，您可以按照以下步骤添加和移除棉绒上的检查:

> 转到**文件>设置>编辑器>检查**，然后勾选您想要棉绒执行的问题检查。

**除绒**

有些情况下，您正在编写危险或容易出错的代码，但是 lint 不会报告任何错误或警告。例如，在安卓工作室中，输入以下代码:

## 我的锅

```kt
fun someUIUpdate() {
   // your UI code goes here
   proceessSomething()
}
fun processSomething() {
    // Geeks for geeks
}
```

前面几行代码不会显示任何错误，尽管它们应该在逻辑上显示一些错误，因为网络请求不应该在用户界面更新期间发出。所以，你能做的就是帮助棉绒。

> **极客提示#3** :是的，如果你辅助棉绒，棉绒会辅助你。

始终尝试在项目中利用注释来帮助 lint 更准确地理解代码。现在写一些你以前做过的，然后检查错误:

## 我的锅

```kt
@UiThread
fun someUIUpdate() {
    // your code bugs here
    processChanges()
}
@WorkerThread
fun processChanges() {
    // Geeks for Geeks
}
```

### 3.使用基线

如果您正在处理一个大型项目，并且希望识别将来在向项目添加附加代码时可能出现的错误，您可以为项目设置一个基线，lint 将创建在该基线之后发生的错误。因此，lint 将忽略以前的代码问题，只提醒您基线之后引入的新代码行。

**要在项目中包含基线，请在 build.gradle 文件中添加以下行:**

```kt
android {
  lintOptions {
    baseline file("lint-geeksforgeeks-example.xml")
  }
}
```

这将生成一个 lint-baseline.xml 文件，作为项目的基线。要添加另一个基线，请再次移除文件和 lint。

### 结论

在本文中，我们学习了如何在安卓工作室中使用 Lint。我们发现，如果我们想检查我们的代码，我们不需要手动操作。安卓工作室提供的代码检查工具 Lint 帮助我们清理代码，并为应用程序开发使用必要且正确的代码。因此，**利用 Lint 消除项目中的各种错误，同时也帮助 Lint 帮助您。**