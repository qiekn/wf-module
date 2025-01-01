# WARFACE MOD SDK V1.4.5

Warface MOD SDK V1.4.5 是基于 CryEngine 3.3.8 开发的编辑器，专为处理 Warface 文件而设计。该编辑器可以兼容 2012 到 2020 年间的游戏文件，若涉及其它年份，可能会由于游戏中新技术的应用而出现兼容性问题。目前，版本 1.4.5 是 Warface MOD SDK 唯一稳定且可用的版本（尽管经过深入检验后发现并不总是如此）。

**WF MOD SDK 的开发者已停止了对其的支持，当前作者仅负责完善编辑器及其文档，并为其开发附加工具。**

![WF MOD SDK 1.4.5 启动窗口](https://github.com/user-attachments/assets/f20b97e8-47dd-4ab4-a3ec-ff0caa293714)

## 如何下载编辑器？

包含修改版 WF MOD SDK 1.4.5 的压缩包随附。您需要下载该压缩包并将其移动到您要安装编辑器的磁盘。解压后会生成两个文件夹，其中的“MSDK_Editor”文件夹内即为编辑器。文件夹“ReadMe”中包含了关于编辑器和其模块的文章，以及来自 WFCRYDOC 官方网站的资料副本和使用指南。

## 如何将 Warface 的对象和纹理导入编辑器？

编辑器能稳定工作的最后一个 Warface 客户端可以通过 [这一链接](https://drive.google.com/file/d/1grepEDHBVGQL9PHTg8w_T2e0DXndHLg3) 下载。如果该客户端不符合您的需求，请查找另一个未分割纹理的客户端（即没有 _.dds.0、_.dds.1 等文件），因为编辑器无法处理这些文件。您需要将该客户端（Game 文件夹中的）所有扩展名为 \[.pak\] 的文件复制到编辑器的 \[MSDK_Editor/Game\] 路径下。注意排除 \[GameInfo.pak\] 和 \[GameScriptsC.pak\]！如果您从链接下载了客户端，PAK 归档文件已经解密，无需再进行其他处理。

## 使用编辑器还需要什么？

为了正常使用编辑器，需要安装所有 DirectX 组件，以及 Microsoft Visual C++。您可以通过以下链接下载所有所需包。

DirectX: https://www.microsoft.com/ru-ru/Download/confirmation.aspx?id=35

Microsoft Visual C++: https://www.techpowerup.com/download/visual-c-redistributable-runtime-package-all-in-one/

## 如何使用编辑器？

您可以通过 \[Bin64\] 文件夹内的 \[Editor.exe\] 启动编辑器。该编辑器几乎完整复现了 CryEngine 3 的功能，相关教程可以在网上轻松找到，也可以在此处查看。

## 编辑器是否存在缺陷？

是的，编辑器确实存在一些缺陷，这可能会影响您使用的体验。以下是已知的问题列表：

1. 与 CryEngine 的默认角色的交互非常不稳定。在尝试调整角色（例如更换外观、武器、动画）时，会出现各种无法解决的问题。然而，有些功能已从旧版本修复，如角色控制和 HUD。我们已解锁了垂直相机移动，去掉了屏幕上的奇怪条纹，并恢复了某些 HUD 功能；
2. 自定义 EnvironmentProbe（CubeMaps）功能无法使用。创建的纹理将无法与实体交互。若要在地图上使用 EnvironmentProbe，必须使用已有的纹理，无法创建自定义纹理；
3. 在处理纹理、保存或导出时，可能会出现严重错误，导致引擎崩溃或强制关闭。因此建议定期保存您的关卡进度，以免造成重大损失。

## 改进建议

如果您知道任何错误信息或解决方案，欢迎在此反馈或联系作者，以便我能在可能的情况下修复这些问题。
