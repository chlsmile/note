## nginx日志切割脚本

```bash

#!/bin/bash

#设置nginx日志存储路径
LOGS_PATH="/data/logs/nginx"

#获取昨天的日期
YESTERDAY=$(date -d "yesterday" +%Y%m%d)

#日志分割，按天分类
LOGS=`ls ${LOGS_PATH}/*.log | xargs -n 1 | cut -f 5 -d "/" | cut -f 1 -d "."`
for LOG in $LOGS
do
  mv ${LOGS_PATH}/${LOG}.log ${LOGS_PATH}/backup/${LOG}-${YESTERDAY}.log
done

kill -USR1 `ps aux | grep nginx | grep master | awk '{print $2}'`

```