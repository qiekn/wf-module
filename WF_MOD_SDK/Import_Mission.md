# 在 WF MOD SDK 1.4.5 中导入和设置关卡内容

在提取了所有关卡内容后，您需要将其导入编辑器，以重新创建地图。这里我将引用并延续之前的“Mission_Extract”指示，以便于理解和使用。

## 导入过程

完成之前的步骤后，您应该在路径 \[MSDK_Editor/Game/Levels/\] 下有一个地图文件夹（以 \[tdm_downtown\] 为例）。在使用转储工具后，希望您已经整理了在 \[MSDK_Editor/Game/Levels/tdm_downtown/Setting/\] 文件夹中生成的文件，方便后续工作。接下来按照以下指示操作：

1. 将地图文件夹（例如 \[tdm_downtown\]）重命名为其他名称，可以在末尾添加数字（例如 \[tdm_downtown1\]）；
2. 接下来，打开编辑器 \[MSDK_Editor/Bin64/Editor.exe\]，创建一个新级别（在顶部菜单 File —> New）；

   2.1 将级别命名为地图的原始名称（我的例子是 \[tdm_downtown\] 不带数字），因此我们在文件夹名中添加数字，以避免编辑器报错；

   2.2 在 \[Heightmap Resolution\] 处，选择与提取的文件名相符的地形尺寸，即 \[dump*terrain*\*\*\*.raw\]，其中星号代表地形边长的数字（例如，文件名为 \[dump_terrain_256.raw\]，在此情况下，选择 \[256x256\]）；

   2.3 在 \[Meters Per Unit\] 选项中始终选择 1；

   2.4 然后点击 \[Ok\];

![image](https://github.com/user-attachments/assets/2b2d273a-774e-4117-8d11-76f09b860e5b)

3. 创建级别后，保存并关闭编辑器。接着需要将所有文件从文件夹 \[tdm_downtown1\] 移动到保存的级别文件夹 \[tdm_downtown\]，然后您可以删除空文件夹。再次启动编辑器并打开级别 \[tdm_downtown\]。
4. 加载级别后，我们需要去除水面（海洋）。为此，找到 \[Edit Terrain\] 选项，点击后在 \[Modify\] 中选择 \[Remove Water\]。由于 Warface 地图通常使用自定义水面，因此不需要水。
5. 现在开始导入地图。首先导入层，以便于看到我们需要飞到的地方，因为相机可能会生成在不同的位置（通常需要朝着原点飞去）。导入层的步骤如下：

   5.1 在菜单 \[Rollup Bar\] 找到 \[Layers\] 选项；

   5.2 点击 \[Import Layers\] 图标；

   5.3 在弹出的窗口中找到地图文件夹，然后进入层文件（我的例子是： \[MSDK_Editor/Game/Levels/tdm_downtown/Setting/Layers/\]）；

   5.4 全选层文件（文件扩展名为 \[.lyr\]），可使用 \[Ctrl + A\] 或鼠标进行选择；

   5.5 点击“打开”，等待加载完成；

6. 加载完毕后，寻找场景中的对象并飞过去；
7. 之后我们需要导入地形，但需要手动将高度图逆时针旋转 90 度，可以使用支持 raw 文件的图形编辑软件（如 Photoshop）：

   7.1 在级别目录的 \[Setting/Terrain/dump*terrain*\*\*\*.raw\] 路径中找到指定文件，并用任何支持 raw 文件的程序打开；

   7.2 将图像逆时针旋转 90 度；

   7.3 用稍微不同的名称（例如：\[dump_terrain_256_90.raw\]）保存到相同路径；

   7.4 在编辑器中，重新打开 \[Edit Terrain\]，在 \[File\] 中选择 \[Import Heightmap\]；

   7.5 选择我们刚保存的旋转文件，点击”打开“并等待加载完成；

8. 现在导入时间（Time Of Day），具体步骤如下：

   8.1 在 \[Terrain\] 标签中找到 \[Time Of Day\] 选项并点击；

   8.2 在弹出窗口中，点击 \[Import From File\]；

   8.3 找到 CLC 提取的文件，路径为 \[Setting/TOD/TimeOfDay.tod\]；

   8.4 点击“打开”，等待加载完成；

9. 然后导入灯光设置：

   9.1 在 \[Edit Terrain Lighting\] 中点击 \[Import\]，并导入路径为 \[Setting/Lighting/LightSettings.lgt\] 的文件；

   9.2 将 \[Time Of Day\] 与文件 \[mission_mission0.xml\] 第一行的 \[Time\] 值保持一致；

10. 现在，您只需输入所需的值，以便为地图赋予真实外观：

    10.1 在菜单 \[Rollup Bar\] 找到 \[Terrain\] ，然后选择 \[Environment\]；

    10.2 打开之前的文件 \[mission_mission0.xml\]；

    10.3 查找 \[\<Environment\>\] 标头并将其所有值转移到编辑器中；

11. 如果您想对地形纹理进行手动绘制（由于目前无法自动恢复），请执行以下步骤：

    11.1 在 \[Edit Terrain Texture\] 中操作；

    11.2 点击 \[File\]，再点击 \[Import Layers...\]；

    11.3 在弹出的文件浏览器中找到 \[MSDK*Editor/Game/Levels/ВАША*КАРТА/Setting/Terrain/\] 下的 \[TerrainLayerTexInfo.lay\] 文件；

    11.4 点击“打开”，这时在 \[Edit Terrain Texture\] 标签中将出现您可以用来通过 \[Rollup Bar\] 中的 \[Terrain\] 选项来绘制地形纹理的各个层；

12. 最后，如果您希望恢复关卡中的植物，可以按照以下步骤操作：

    12.1 在 \[Rollup Bar\] 中找到 \[Terrain\] 选项，并点击 \[Vegetation\]；

    12.2 点击 \[Import Vegetation\] 图标并导入路径为 \[Setting/Vegetation/VegetationObject.veg\] 的文件；

    12.3 这时将会出现植被对象列表，您需要手动摆放这些对象，确切的坐标可以在路径为 \[Setting/Vegetation/veg_dump.txt\] 的文件中找到。

## 总结

至此，地图导入过程已结束。现在您手中有了一个几乎完整的 CRY 级别文件，可继续进行编辑和学习。下一步将在 "Export_Mission" 中学习如何将地图导入游戏并进行游戏体验。

```
`
```
