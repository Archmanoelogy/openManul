# OpenManul编辑说明

OpenManul是一个开放动物园展览动物数据集，旨在呈现动物个体的饲养情况及其个体之间的亲缘关系，并尽可能地保证数据的可备份、可恢复性。任何人可以在任何时间备份任何一个版本的OpenManul数据，以便在网络访问存在困难或者运营商停止存储服务时通过自己的备份数据还原出数据全貌。任何人可以通过git创建数据库分支，并在自己的分支上修改这个数据集，也可以通过提交pull request将自己对数据集的修改申请合并到这里。

本数据集由yaml文件以特定目录结构组织而成，yaml文件内部的结构遵循ID+信息的结构，动物个体、动物园、血缘信息、图片资源都通过唯一的ID进行关联，ID的格式、yaml文件的格式和其他修改注意事项见此说明书的具体章节。

本数据集的数据结构服务于网站的呈现，主分支数据集的数据呈现在[这个网址](https://manul.apiglio.top)；这个网站由专门的[openManulServer项目](https://github.com/Archmanoelogy/openManulServer)实现，可以在任何常见PC设备上通过安装python3实现和网站相同的本地部署。该项目同时可以判断数据集修改后是否完整有效，如果您希望将自己修改的版本合并到这里，十分建议按照此项目的指引在本地测试，保证提交的数据的结构完整性。

## 数据集结构

所有数据保存在`data`目录下，使用yaml格式。`data/zoo`目录下存放动物园等空间信息，`data/individuals`目录下存放动物个体信息，预留了`manul`以外的其他物种数据目录。

动物园或动物个体都包含自身的ID、基本名称信息和其他详细信息，其中个体和动物园的ID、名称信息、别名，以及动物园的地理坐标，均保存在`names.yaml`文件，其他信息保存在`information.yaml`中。个体之间的血缘关系信息保存在`litter.yaml`中。如果ID存在变更的情况，记录在`former_id.yaml`中。动物个体的图片存档保存在`image`目录中，图片文件名和`image_credit.yaml`中的图片ID对应。

与修改`data`数据相关的指引文件存放在`instructions`目录下，使用markdown格式。

```
.
├── .gitignore
├── .gitattributes
├── data
│   ├── zoo
│   │   ├── names.yaml
│   │   └── information.yaml
│   └── individuals
│       ├── manul
│       │   ├── names.yaml
│       │   ├── information.yaml
│       │   ├── litter.yaml
│       │   ├── former_id.yaml
│       │   ├── image_credit.yaml
│       │   └── image
│       │       └── {ImgID}.png
│       └── other species ...
└── instructions
    ├── readme.zh.md
    └── ...
```

## 不同数据类型及其修改格式

### ID

每个动物个体拥有唯一不重复的ID，个体ID的标准格式是`名称_出生年份`，名称采用动物个体所在地的语言罗马化形式，只允许出现拉丁字母`A`～`Z`和半角连字符`-`，不区分大小写；出生年份信息为4位数字。

无法确定出生年份而又确实需要收录这一个体时：

1. 野外个体无法确定的情况用`wild`代替四位年代数字，例如`Zelenogorsk_wild`；

2. 可能通过进一步调查确定出生年份时暂时用`temp`代替，例如`Karaganda_temp`，并在确定出生时间后将这个ID转存到`former_id.yaml`中，并做好别名映射。

同年同名时：

1. 优先考虑本地化的罗马化方案，例如`Princess`和`Prinsessa`；

2. 无法通过以上方法区分时引入地点，例如`Boris-in-Budapest`或`Boris-in-BCR`。

### 链接

### 文本描述

### 日期

### 图片资源
