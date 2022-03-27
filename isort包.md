# Python中isort包的使用

isort包是一个使import 列表更美观的工具包，官方例子如下：

## 使用前
```
from my_lib import Object
print("Hey")
import os
from my_lib import Object3
from my_lib import Object2
import sys
from third_party import lib15, lib1, lib2, lib3, lib4, lib5, lib6, lib7, lib8, lib9, lib10, lib11, lib12, lib13, lib14
import sys
from __future__ import absolute_import
from third_party import lib3
print("yo")
```
## 使用后
```
from __future__ import absolute_import
import os
import sys
from third_party import (lib1, lib2, lib3, lib4, lib5, lib6,lib7, lib8,lib9, lib10, lib11, lib12, lib13, lib14, lib15)
from my_lib import Object, Object2, Object3
print("Hey")
print("yo")
```
## 使用isort包
从命令行：
```
isort mypythonfile.py mypythonfile2.py
```
或者递归输入：
```
isort -rc .
```
这等价于：
```
isort **/*.py
```
or to see the proposed changes without applying them:
```
isort mypythonfile.py --diff
```
Finally, to atomically run isort against a project, only applying changes if they don‘t introduce syntax errors do:
```
isort -rc --atomic .
```