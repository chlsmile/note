## 在shell脚本中获取并输出当前git分支名
```bash

#!/bin/sh

branch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')

echo "当前分支 "$branch

```