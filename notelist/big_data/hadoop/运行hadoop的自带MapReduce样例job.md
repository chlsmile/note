## 运行hadoop的自带MapReduce样例job

#### Make the HDFS directories required to execute MapReduce jobs
```bash
$ bin/hdfs dfs -mkdir /user
$ bin/hdfs dfs -mkdir /user/<username>
```

#### Copy the input files into the distributed filesystem:
```bash
$ bin/hdfs dfs -put etc/hadoop input
```

#### Run some of the examples provided:
```bash
$ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.8.4.jar grep input output 'dfs[a-z.]+'
```

#### Examine the output files: Copy the output files from the distributed filesystem to the local filesystem and examine them:
```bash
$ bin/hdfs dfs -get output output
$ cat output/*
```

#### or View the output files on the distributed filesystem:
```bash
 $ bin/hdfs dfs -cat output/*
```
