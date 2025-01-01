# 创建迷你地图

## 教程

当你创建好自己的关卡后，需要为其创建迷你地图。创建它很简单，只需执行以下步骤：

1. 启动编辑器并加载关卡，并将视角抬高至足够能看到整个地图的高度；
2. 在 RollupBar 菜单中，切换到 `Terrain` 选项卡，并选择 `Mini Map`；
3. 在 `Resolution` 项中选择期望的迷你地图的尺寸，从 8x8 到 8192x8192 像素（建议不要超过 4096x4096）；
4. 然后在地形上会出现蓝色和绿色的方框，你可以用鼠标移动它们，无需理会蓝色方块，你需要根据绿色方块来定位，因为它负责定义你的迷你地图的边界；
5. 在 `Camera Height` 项中选择相机的高度，也即它的范围，这就是绿色方块的尺寸；
6. 在 `Output` 项中，输入导出文件名，你可以取消 TIF 文件的勾选，因为 Warface 只需要 DDS 文件；
7. 点击 `Generate MiniMap` 按钮，等待处理完成；
   ![image](https://github.com/user-attachments/assets/45cd968d-22e7-42f4-980b-52b1b12de5e8)

8. 然后，你需要找出地图的北方，可以通过右上角透视图信息显示的值来完成。然后在这些数字和字母中寻找词 `Angl=` 并数取第三个数字，它就是北方的指示器。你需要转动相机，使该值等于零，在此值下你的相机正对北方。接下来将相机向下移动并记住关键对象的位置；
   ![image](https://github.com/user-attachments/assets/581c51d4-6d0f-4cce-b43c-6e349086ece1)

9. 现在进入地图文件夹，找到已生成的 DDS 图像，打开它（最好使用 Paint net，因为它在这方面更加方便），并将北方位置与你在相机指向北方时所记住的位置进行比较，如果北方向上方位置一致则一切正常，如果不一致，请将图像旋转以确保地图的北方在图像的顶部；
   ![image](https://github.com/user-attachments/assets/02fba868-688d-4039-afa3-4a82de5182cd)
   ![image](https://github.com/user-attachments/assets/f60afe3a-9df6-4264-979a-9392fd5d329b)

10. 之后保存图像；
11. 现在需要处理其技术部分。与迷你地图图像一起生成其 XML 文件，其中记录显示在游戏中正确预览的参数，但编辑器未添加一个重要行，你需要手动添加。标准文件如下所示：

```xml
<MetaData>
<Setting name="pvp/tdm_downtown" />
  <MiniMap Filename="tdm_downtown.dds" startX="50.011246" startY="38.981354" endX="190.01125" endY="178.94135" width="2048" height="2048"/>
</MetaData>
```

![image](https://github.com/user-attachments/assets/cc98170c-389c-4323-8b95-adc1f7e4c524)

你还需要添加另一行：

![image](https://github.com/user-attachments/assets/b083873b-7ae8-4aef-b489-354237ff15ad)

其中 `name` - 你迷你地图在 `Levels` 文件夹中的路径。因此，你只需将路径插入其中即可。

行：`<Setting name="Path/level"/>`

15. 然后返回编辑器并保存级别，以确保文件中的尺寸正确保存至 `filelist.xml`。

## 总结

这就是全部了，您已经创建了自己的迷你地图，现在您可以用《Warface》相同的风格重绘它，或者保持不变，但请记住，在每次更改迷你地图文件后，您需要在编辑器中重新保存关卡。
