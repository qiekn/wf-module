# CryLevelConvert、CryDumper 和 Mission_Extract | 提取 Warface 关卡内容

通过 CryLevelConvert（以下简称为“CLC”）、CryDumper（以下简称为“转储工具”）和 Mission_Extract 的组合，您可以提取以下关卡数据：

1. 动态实体（包括实体原型）；
2. 流程图（关卡动态图形代码）；
3. 时间轴（关卡轨迹）；
4. 时间数据（TimeOfDay）；
5. 地形纹理层；
6. 静态几何体；
7. AI 导航（AI 锚点，AIPoint）；
8. 地形高度图（Terrain）；
9. 植被坐标（Vegetation）；
10. 植被数据（Vegetation）；
11. 地形光照工具的数据（Terrain Lighting Tool）；
12. 自定义对象的 CGF 文件（Solid）。

了解每个工具的功能非常重要。CLC 用于提取以上列表中的第 1-5 项。第 6-9 项由转储工具负责。而第 10-12 项及 CLC 的正确运行和后续文件整理则由 Mission_Extract 负责。

## 如何找到程序数据？

这些程序和其组件（CLC、转储工具和 Mission_Extract）都包含在 WF MOD SDK 编辑器中。CLC 和 Mission_Extract 位于 \[MSDK_Editor/CryLevelConvert/\] 路径下，而 CryDumper 则在 \[MSDK_Editor/Bin64/\] 路径下。

## 在开始工作之前需要准备些什么？

是的，为了确保 CLC 正常工作，您需要找到并将 \[EntityArchitypes\] 文件夹转移到 \[MSDK_Editor/CryLevelConvert/\]。该文件夹位于游戏存档的 \[Game/GameData.pak/Libs/\] 路径下。同时，您还需要确保所需的关卡资源已经包含在您的客户端中。如果您想要提取 2019 年的某个地图，而您的客户端是 2018 年的，由于缺少必要的资源或实体原型数据，可能会导致关卡提取不完整，或者在转储工具阶段出现错误。因此，请在开始工作之前确认客户端的有效性。

## 如何使用这些程序？

请遵循以下步骤：

1. 在游戏文件夹中找到要提取的地图（地图应在 2020 年之前开发）；
2. 确定地图后，复制该地图文件夹中的 pak 归档 \[level.pak\] 到以下路径：\[MSDK_Editor/CryLevelConvert/\]；
3. 如果需要，使用 PakDecrypt 解压 \[level.pak\]。解压后会生成文件 \[level.pak.zip\]，您需删除原始的 \[level.pak\] 并将 zip 归档重命名为 \[level.pak\]（即去掉扩展名 \[.zip\]）；
4. 接下来，运行 \[Mission_Extract.exe\] 并按照程序指示操作；
5. 程序运行的结果会生成一个以地图命名的文件夹，您需要将该文件夹移动到 \[MSDK_Editor/Game/Levels/\] 文件夹中；
6. 然后寻找 \[CryDumper.exe\]，该文件位于 \[MSDK_Editor/Bin64/\] 文件夹中。启动它后，您应该能看到 CryEngine 控制台。输入命令： `map Name_Level`

> Name_Level（地图名称）—— 您可以在您提取的地图文件夹中找到（例如：`map tdm_downtown`）。

7. 现在，按下 Enter。完成过程后，您将在 \[MSDK*Editor\] 中获得以下文件： \[ai_points_dump.lyr\]、\[clc_brushes_layer.lyr\]、\[dump_terrain*\*\*\*.raw\]、\[veg_dump.txt\]。
8. 所有数据文件需要移动到地图文件夹 \[MSDK_Editor/Game/Levels/你的地图/Setting/\] 中，并建议根据已有的文件夹进行整理；

恭喜您！您已经提取了当前关卡的所有可能内容。

## 参考来源

部分文档材料源自被移除的 [WFCRYDOC](https://wfcrydoc.fandom.com/ru/wiki/CryLevelConvert_и_CryDumper) 网站。作者不主张对原始材料的拥有权。

CryLevelConvert 文档：https://github.com/prophetl33t/CryLevelConvert

Mission_Extract 文档：https://github.com/wfom/Mission-Extract
