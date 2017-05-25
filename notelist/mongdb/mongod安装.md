## Install MongoDB Community Edition From Tarball


##### 1.Download the binary files for the desired release of MongoDB

```
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.4.tgz
```

##### 2.Extract the files from the downloaded archive
```
tar -zxvf mongodb-linux-x86_64-3.0.4.tgz
```

##### 3.Copy the extracted archive to the target directory
```
- mkdir -p mongodb
- cp -R -n mongodb-linux-x86_64-3.0.4/ mongodb
```

##### 4.Ensure the location of the binaries is in the PATH variable

The MongoDB binaries are in the bin/ directory of the archive. To ensure that the binaries are in your PATH, you can modify your PATH.

For example, you can add the following line to your shell’s rc file (e.g. ~/.bashrc):

```
export PATH=<mongodb-install-directory>/bin:$PATH
```


## Run MongoDB Community Edition

##### 1.Create the data directory

Before you start MongoDB for the first time, create the directory to which the mongod process will write data. By default, the mongod process uses the /data/db directory. If you create a directory other than this one, you must specify that directory in the dbpath option when starting the mongod process later in this procedure

The following example command creates the default /data/db directory:

```
mkdir -p /data/db
```

##### 2.Set permissions for the data directory
Before running mongod for the first time, ensure that the user account running mongod has read and write permissions for the directory

##### 3.Run MongoDB

Run MongoDB.

To run MongoDB, run the mongod process at the system prompt. If necessary, specify the path of the mongod or the data directory. See the following examples

**Run without specifying paths**

If your system PATH variable includes the location of the mongod binary and if you use the default data directory (i.e., /data/db), simply enter mongod at the system prompt:

```
mongod
```

**Specify the path of the mongod**

If your PATH does not include the location of the mongod binary, enter the full path to the mongod binary at the system prompt:

```
<path to binary>/mongod
```

**Specify the path of the data directory**

If you do not use the default data directory (i.e., /data/db), specify the path to the data directory using the --dbpath option:

```
mongod --dbpath <path to data directory>
```

