# 为 CryEngine 和 Warface 创建 PAK 压缩包

## 创建流程

要创建正确的 PAK 压缩包，文件必须以正确的方式进行压缩。并不是所有的传统压缩软件都能做到这一点，这会导致文件对引擎和游戏不可读。因此，您需要使用程序\[7za.exe\]，它是编辑器的一部分，位于\[MSDK_Editor/Tools/CryArchiver/\]。具体步骤如下：

1. 将程序文件夹移动到您方便的位置；
2. 将需要打包的文件或文件夹移入程序文件夹；
3. 打开命令提示符或 PowerShell；
4. 输入命令：cd "程序在您系统中的完整路径"（无引号）并按 Enter；

   4.1 例如： `cd C:\CryEngine\WF_MOD_SDK\MSDK_Editor\Tools\CryArchiver\`

5. 然后输入以下命令：

   5.1 对于命令提示符（文件夹）：`7za a -tzip -mx0 -r 名称_压缩包.pak 名称_文件夹\*.*`

   5.2 对于命令提示符（文件）：`7za a -tzip -mx0 -r 名称_压缩包.pak 名称_文件.xxx`

   5.3 对于命令提示符（多个文件和文件夹）：`7za a -tzip -r -mx0 名称_压缩包.pak 名称_文件1.xxx, 名称_文件2.xxx 名称_文件夹1\*.* 名称_文件夹2\*.*`

   5.4 对于 PowerShell，在命令前添加`.\`

6. 您的 PAK 压缩包已准备好！（它将出现在与程序相同的文件夹中）。

## 命令参数说明

`7za` - 程序名称；

`a` - 将文件添加到压缩包中（如果压缩包不存在，则创建并添加，支持文件替换）；

`-tzip` - 压缩包类型（在这里是 zip）；

`-mx0` - 压缩级别（为 0 时，文件以无压缩方式打包）；

`-r` - 递归子目录（具体用法还需确认）；

`名称_压缩包.pak` - 您想要的压缩包名称（对于 CryEngine 和 Warface，必须带拓展名\[.pak\]）；

`名称_文件夹\*.*` - 指定要打包的文件夹，_._ 表示打包其全部内容；

`名称_文件.xxx` - 要打包的文件名称（`xxx`为文件拓展名，必需！例如：`test.xml`）；

如果您想同时打包多个文件和文件夹，则文件以逗号分隔，文件夹以空格分隔。

## 使用示例

压缩文件夹：`7za a -tzip -mx0 -r 纹理.pak 纹理\*.*`

压缩文件：`7za a -tzip -mx0 -r 纹理.pak sky.dds`

压缩文件夹和文件：`7za a -tzip -r -mx0 纹理.pak sky_day.dds, sky_night.dds 纹理\cubemaps\*.* 纹理\decals\*.*`

# 7za.exe 程序简要说明

## 描述

7za - 一款具有极高压缩比的文件压缩工具。这是一个独立执行文件。7za 支持的压缩格式较少，无法与 7z 相比。

7-Zip - 是一款具有最高压缩比的文件压缩工具。该程序支持多种格式，包括 7z（实现了 LZMA 压缩算法）、LZMA2、XZ、ZIP、Zip64、CAB、RAR（安装了 p7zip-rar 包后支持）等。新格式 7z 的压缩比比 ZIP 格式高出 30-50%。

## 功能字母

`a` - 添加

`d` - 删除

`e` - 提取

`l` - 列表

`t` - 测试

`u` - 更新

`x` - 以完整路径提取

## 切换参数：

`-ai[r[-|0]]{@listfile|!wildcard}` - 包含压缩包

`-ax[r[-|0]]{@listfile|!wildcard}` - 排除压缩包

`-bd` - 禁用百分比指示器

`-i[r[-|0]]{@listfile|!wildcard}` - 包含文件名

`-l` - 不保留符号链接；保留指向的文件/文件夹（注意：扫描阶段可能会因递归符号链接而永远无法完成）

`-m{Parameters}` - 设置压缩方法（详见 /usr/share/doc/p7zip-full/DOCS/MANUAL/switches/method.htm 中的方法列表）

`-mhe=on|off` - 仅限 7z 格式：启用或禁用压缩包头部加密（默认为禁用）

`-o{Directory}` - 设置输出目录

`-p{Password}` - 设置密码

`-r[-|0]` - 递归子目录（注意：此标志不一定如预期使用，请谨慎）

`-sfx[{name}]` - 创建 SFX 压缩包

`-si` - 从标准输入读取数据（例如：tar cf - 目录 | 7za a -si 目录.tar.7z）

`-so` - 将数据写入标准输出（例如：% echo foo | 7z fakefile -tgzip -si -so > /dev/null）

`-slt` - 为 l 命令（列出）设置技术模式

`-t{Type}` - 压缩包类型（7z, zip, gzip, bzip2 或 tar. 7z 为默认）

`-v{Size}[b|k|m|g]` - 创建卷

`-u[-][p#][q#][r#][x#][y#][z#][!newArchiveName]` - 更新参数

`-w[path]` - 设置工作目录

`-x[r[-|0]]]{@listfile|!wildcard}` - 排除文件名

`-y` - 假定所有提问为“是”

## 诊断

7-Zip 返回以下退出代码：

`0` - 正常（无错误或警告）

`1` - 警告（无法解决的错误，例如某些文件在压缩过程中无法读取，未被压缩）

`2` - 致命错误

`7` - 命令行参数错误

`8` - 内存不足

`255` - 用户通过 control-C（或类似方式）停止了进程

## 备份与限制

请勿在 Linux/Unix 上使用 7-Zip 格式进行备份，因为：

- 7-Zip 不会保留文件的所有者/组。

在 Linux/Unix 中，要备份目录应使用 tar：

- 创建目录备份：tar cf - directory | 7za a -si directory.tar.7z

- 恢复备份：7za x -so directory.tar.7z | tar xf -

如果您希望将文件与目录（而非文件所有权）发送给其他 Unix/macOS/Windows 用户，则可以使用 7-Zip 格式。

- 示例：7za a directory.7z directory

请勿使用“-r”标志，因为此标志不会如想象般工作。

请勿使用 directory/_，因为会有“._”文件（例如：“directory/\*”不匹配“directory/.profile”）。

## 关于 CryPak 系统的相关文章

[https://docs.cryengine.com/display/SDKDOC4/CryPak](https://www.cryengine.com/docs/static/engines/cryengine-3/categories/1638401/pages/1605659)

[https://docs.cryengine.com/display/SDKDOC4/Accessing+Files+with+CryPak](https://www.cryengine.com/docs/static/engines/cryengine-3/categories/1638401/pages/15010579)
`
