# H5GG特征码搜索工具
工具基于<a href="https://githubfast.com/H5GG/H5GG">H5GG</a>引擎制作，用于快速找到已知数值，无需模糊搜索或其他操作，也可用于脚本中，例如<br/>
```javascript
h5gg.searchNumber('114514', 'U32', '0x000000000', '0x160000000');
h5gg.searchNearby('1919810', 'U32', '0x4');
h5gg.searchNumber('114514', 'U32', '0x000000000', '0x160000000');
h5gg.searchNearby('1145141919810', 'U32', '0x8');
h5gg.searchNumber('114514', 'U32', '0x000000000', '0x160000000');
Results = h5gg.getResults(1);
addr = Number(Results[0].address) + 0x16;
```
## 使用方法
首次进入APP，在通过模糊搜索等方法找到需要扫描的值后，点击**首次扫描**，输入该数值对应的**地址**、**类型**以及允许**特征码**与**该值地址**的**最大偏移**。首次扫描采集到的此范围内的所有值会以**JSON**的形式输出，例如<br/>
```json
[{"offset":-224,"value":"0"},{"offset":-208,"value":"2"},{"offset":-176,"value":"2"},{"offset":-48,"value":"1"},{"offset":-44,"value":"131074"},{"offset":-40,"value":"1"},{"offset":-36,"value":"0"},{"offset":-16,"value":"1"},{"offset":-12,"value":"7"},{"offset":-8,"value":"1"},{"offset":0,"value":"98312"},{"offset":16,"value":"1"},{"offset":24,"value":"1"},{"offset":28,"value":"4294967295"},{"offset":32,"value":"4294967295"},{"offset":96,"value":"0"},{"offset":100,"value":"0"},{"offset":104,"value":"0"},{"offset":128,"value":"0"},{"offset":196,"value":"0"},{"offset":200,"value":"0"},{"offset":232,"value":"0"},{"offset":256,"value":"0"}]
```
将此地址复制粘贴到备忘录，然后**重启**游戏。**再次**通过模糊搜索等方法找到需要扫描的值，点击**筛选**，输入复制保存的**JSON数据**，以及***与首次扫描相同的类型、地址和最大偏移***，经过筛选后，两次扫描中偏移量和数值都相同的结果会再次以**JSON**的形式输出，经过两次扫描后筛选的结果已经可以使用，可以点击**JSON转文字**来将其转换为**文字结果**，例如<br/>
```text
[212]Offset:-0x3c Value:-131072
[213]Offset:-0x2c Value:6144
[214]Offset:-0x24 Value:1
[215]Offset:-0x1c Value:1
[216]Offset:-0x14 Value:1
[217]Offset:-0xc Value:1
[218]Offset:-0x4 Value:1
[219]Offset:0x4 Value:-131072
[220]Offset:0xc Value:-131072
[221]Offset:0x14 Value:1
[222]Offset:0x18 Value:2
[224]Offset:0x24 Value:6144
```
当然，多次筛选后的结果会**更加精准**。
