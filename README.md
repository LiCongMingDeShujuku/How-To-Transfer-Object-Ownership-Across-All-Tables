![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 如何在所有选项中传输对象所有权
#### How To Transfer Object Ownership Across All Tables


![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
假设你正在进行一次数据库迁移，并发现自己在2012年后再次更改了Object Ownership 即Schema Ownership。这里有一些将所有对象所有权转移到DBO的快速逻辑。或者，你可以简单地将'dbo'改为另一个名字，但目前，我们将在这个例子中使用DBO。


## English
Suppose you’re doing yet another database migration and find yourself again changing the Object Ownership aka Schema Ownership in the post 2012 world… Here’s some quick logic to transfer all object ownership to DBO. Alternatively you can simply change ‘dbo’ to another name, but for the moment; we’ll be using DBO in this example.

---
## Logic
```SQL
use mydatabase;
set nocount on
 
declare @set_new_schema  varchar(max)
set     @set_new_schema  = ''
select  @set_new_schema  = @set_new_schema +
'alter schema dbo transfer ' + table_schema + '.' + table_name + '';' char(10)
from information_schema.tables where table_schema = 'MyOldUserName'
 
exec    (@set_new_schema)
```

Next just run a quick query to confirm.

接下来只需运行快速查询即可确认。

```SQL
1	select table_schema, table_name from information_schema.tables order by table_schema asc
```

If you’re looking to see whats statements are being run first; just run the following:

如果你想知道最先运行的是什么语句; 只需运行以下命令：

```SQL
set nocount on
 
declare @set_new_schema  varchar(max)
set     @set_new_schema  = ''
select  @set_new_schema  = @set_new_schema +
'alter schema dbo transfer ' + table_schema + '.' + table_name + '';' char(10)
from information_schema.tables where table_schema = 'MyOldUserName'
 
select    (@set_new_schema) for xml path(''), type

```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

