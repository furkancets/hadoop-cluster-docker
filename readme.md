## 1. ls 
lists hdfs files and folders

`/user` is home directory of users like `/home` in linux. In this case our hdfs home is `/user/train`

## 2. mkdir 
creates hdfs directory

## 3. put  
copies files and folders from local to hdfs.  

# 4. mv  
moves hdfs files/folder to another directory.

## 5. cp  
copies hdfs files/folders to another directory.

## 6. chown
changes ownership of file/folder.

## 7. chmod
changes access rights of file/folder.

## 8. get
downloads a file/folder form hdfs to local.

## 9. du
shows size of folder.

## 10. rm
deletes file/folder from hdfs.  
For folders `-r`  
For skipping trash `-skipTrash`  

## 11. head, tail, cat to read files.

## 12. User Interface of namenode 
http://localhost:9870/

yarn jar /opt/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar pi 10 15

### 1. Prepare for Map-Reduce job (linux)
- Create a folder for jar and fruit file
```
mkdir mapreduce_example
cd mapreduce_example/
```
- Copy jar and fruit file from physical machine to vm into my_big_data folder using scp or MobaXterm UI

- Now they are in vm
```
ls
dried_fruits.txt  mapreduce.wordcount.jar
```

- Connect namenode and create a folder in hdfs for input to map-reduce job 
```commandline
docker exec -it namenode /bin/bash
 
hdfs dfs -mkdir -p /user/hadoop/datasets/dried_fruits_input
```


- Copy fruits file to first namenode container then hdfs (linux)
```commandline
docker cp dried_fruits.txt namenode:/tmp
docker cp mapreduce.wordcount.jar namenode:/tmp
hdfs dfs -put /tmp/dried_fruits.txt /user/hadoop/datasets/dried_fruits_input
```



### 2. Run MapReduce job

- Submit mapreduce job
```
yarn jar /tmp/mapreduce.wordcount.jar \
com.veribilimiokulu.mapreduce.MR2WordCount \
/user/hadoop/datasets/dried_fruits_input \
/user/hadoop/datasets/dried_fruits_out
```
- See http://localhost:8088/cluster/apps/ACCEPTED in accpted state.  


### 3. See the application outputs  
```
hdfs dfs -cat /user/hadoop/datasets/dried_fruits_out/part-r-00000                                                                                 CASHEW  6186
GRAPE   7716
HAZELNUT        7842
PEANUT  1866
PISTACHIO       2244
RAW HAZELNUTS   1866
WALNUT  13020
```
 