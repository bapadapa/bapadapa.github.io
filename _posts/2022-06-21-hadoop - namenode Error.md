---
layout: single
title: "JournalNode - Incompatible namespaceID for journal Storage"
categories: hadoopEchoSystem
tag: [Linux, Centos, Hadoop, Error]
---

# Error ?

```shell
Incompatible namespaceID for journal Storage Directory /data/hadoop/hdfs/journal/testclusterHa: NameNode has nsId 1209982631 but storage has nsId 1446085514
```

```shell
Incompatible clusterID for journal Storage Directory /data/hadoop/hdfs/journal/testclusterHa: NameNode has clusterId
'CID-cdafe95f-507f-4954-bc79-b20415684c79' but storage has clusterId 'CID-27fe5fd2-6900-4dbf-9ec6-966c48112586'
```

위와 같은 Error가 발생하거나

혹은

DataNode 는 5개인데

Namenode 1(active)에 3개,

Namenode 2(standby)에 2개의 DataNode가 잡힘

# 원인 ?

여러 원인이 있을 수 있다.

Format을 이미 한 상태에서 다시 Format을 사용하여 꼬일 수 있고,

초기화시 NN1에서 Format 후 NN2 에서 bootstrapstandby를 해주어야 하는데 Format을 해주면 위와 같은 문제가 발생할 수 있다.

즉, 버전/ID 정보가 꼬였다는 것

# 해결방법

namespaceID는 아래와 같이 변경해준다.

> JournalNode의 경우 해당하는 경로에 들어가서 아래와 같이 변경해주면 된다.

![image](https://user-images.githubusercontent.com/53324492/174823400-7bbd2b26-9f35-4e4d-9574-be32da49d604.png)

![cluster id 1](https://user-images.githubusercontent.com/53324492/174823500-926549e3-9e70-4885-9691-ec334b506fdd.png)

> Datanode의 경우 아래와 같이 Web은 들어가지니, 확인하고 변경해주면 된다.

![cluster id 2](https://user-images.githubusercontent.com/53324492/174823822-ce2b461a-acc4-47da-96c8-287a31d1a809.png)

위와같은 방법을 할 줄 모르겠다면, 아래와 같이 본인이 지정한 Namenode 경로를 들어가 VERSION안의 내용을 확인 후 맵필해주면 된다. (옛날에 캡쳐한거라, 버전 정보가 다르다.)

![NameNode Version](https://user-images.githubusercontent.com/53324492/174824526-ca5e628c-4cf2-45c1-a4a5-edfc3de88213.png)

# 결론

1. 실행 순서를 지키라는 말은 괜히 있는게 아니다.
1. 하나하나 차근차근해서 실수하지말자.
1. 버전 정보를 잘 맞추자.
