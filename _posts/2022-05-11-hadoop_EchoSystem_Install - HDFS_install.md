---
layout: single
title: "CentOS7_HDFS_Install"
categories: hadoopEchoSystem
tag: [Linux, Centos, Install, Hadoop, EcoSystem, HDFS]
---

{% capture my_index %}{%include_relative index/hadoop_echosystem_install.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# 다운로드 및 설치

필자는 회사에 구축되어 있는 것을 기준으로 구축을 재 구축을 해야 해서 , **`2.7.3 버전`**을 이용 및 **`HA 구성`**하여 설치를 진행했다

각자 원하는 버전을 이용하여 설치하면 될 것 같다.

[공식 아파치 아카이브](https://archive.apache.org/dist/hadoop/) 이곳에 들어가서 원하는 경로에 맞게 설치해주면 된다.

```sh
wget https://archive.apache.org/dist/hadoop/core/hadoop-2.7.3/hadoop-2.7.3.tar.gz
# 만약 원하는 설치 경로가 존재한다면 -C 옵션을 이용하여 해당 경로로 압축 해제를 해도 된다.
tar xvfz hadoop-2.7.3.tar.gz
```

# SSH

HDFS는 SSH를 이용하여 통신하기 때문에 필수
HA구성할 Server들과 모두 교환한다.

최초 연결 시 비밀번호를 기입하라 하기 때문에, 각각 1번씩은 연결시켜준다.

```shell
<!– 키 생성 -->
 ssh-keygen
<!– 키 배포 -->
 ssh-copy-id [USER]@[HDFS_Server_2]
 ssh-copy-id [USER]@[HDFS_Server_3]
```

설명은 잘 못하지만, [SSH]({{site.url}}/linux/Linux-SSH)를 간략하게 정리하여 포스팅 한 곳이 있으니 원한다면 읽어보세요

# 설정

## {Hadoop, mapred, ,yarn}-env.sh 추가

```sh
# 굳이 아래와 같이 할 필요는 없다.
# 올바른 경로만 잘 넣어주면 된다.
export JAVA_HOME=$(readlink -f $(which java) | sed "s:/bin/java::")
export HADOOP_HOME=$(readlink -f $(which hadoop) | sed "s:/bin/hadoop::")
```

> 위 값을 .bashrc에 삽입하여 사용해도 되지만, 해당 User가 아니면 설정이 되지 않기 때문에 필자는 ~env.sh 에 삽입해줌

## core-site.xml

```xml
<configuration>
 <!-- Master Node-->

 <name>fs.defaultFS</name>
 <value>hdfs://bapaHa</value>

 <!-- 구성한 주키퍼서버 저장 -->

 <name>ha.zookeeper.quorum</name>
 <value>h1:2181,h2:2181,h3:2181</value>

</configuration>
```

\<value>hdfs://bapaHa\</value> 이 부분은 원하는 hdfs이름을 작성해 주면 된다.

e.g \<value>hdfs://abcdHa\</value>

## hdfs-site.xml < HDFS 관련 내용 >

```xml
<!-- replication , namenode , journalnode 등 HDFS에 관한 내용을 설정함 -->

<!--Replica Nums -->
<property>
  <name>dfs.replication</name>
  <value>3</value>
</property>
<property>
  <name>dfs.name.dir</name>
  <value>file:///hadoop/hdfs/namenode</value>
</property>
<property>
  <name>dfs.data.dir</name>
  <value>file:///hadoop/hdfs/datanode</value>
</property>
<!-- 나머지 내용은 너무 길어 패스함 -->

```

## mapred-site.xml < MapReduce 관련 내용 >

```xml
 <!-- Framework 내용 -->
<name>mapreduce.framework.name</name>
<value>yarn</value>
<!-- 필요에 따라 설정하면 된다. -->
<name>yarn.app.mapreduce.am.env</name>
<value>HADOOP_MAPRED_HOME=$HADOOP_HOME</value>

<name>mapreduce.map.env</name>
<value>HADOOP_MAPRED_HOME=$HADOOP_HOME</value>

<name>mapreduce.reduce.env</name>
<value>HADOOP_MAPRED_HOME=$HADOOP_HOME</value>

<!– 메모리 등을 필요시 아래와 같이 설정 -->
 <name>mapreduce.map.memory.mb</name>
 <value>256</value>

 <name>mapreduce.reduce.memory.mb</name>
 <value>256</value>

 <name>mapreduce.map.java.opts</name>
 <value>-Xmx256m</value>

 <name>mapreduce.reduce.java.opts</name>
 <value>-Xms256m</value>
```

## yarn-site.xml < Yarn 관련 내용 > 상세 내용은 너무 길기 때문에 패스

```xml
<!– Yarn HA 구성여부 -->
<property>
    <name>yarn.resourcemanager.ha.enabled</name>
    <value>true</value>
</property>
<!-- hdfs.xml에서 설정한 dfs.nameservices -->
<property>
    <name>yarn.resourcemanager.cluster-id</name>
    <value>shbHa</value>
</property>
<!-- 사용할 resourcemanager 개수 만큼 이름 삽입 -->
<property>
    <name>yarn.resourcemanager.ha.rm-ids</name>
    <value>rm1,rm2</value>
</property>
<!-- 그에 관한 내용은 아래에 기입 -->
<!-- 나머지 내용은 너무 길어 패스함 -->

```

# HDFS 테스트

## 실행

```bash
# 아래와 같이 실행시켜도 되지만, JournalNode, ZKFC, JobHistoryServer가 실행되지 않는다.
sbin/start-all.sh
```

> HA 구성시 권장 실행 순서, 종료시 역순으로 종료 시킨다.

```bash
bin/hdfs journalnode

bin/hdfs namenode

bin/hdfs zkfc

bin/hdfs datanode

sbin/start-yarn

bin/yarn resourcemanager

bin/mapred historyserver

```

## FS 상태 확인

```bash
[root@hdfsserver1 ~]# hdfs dfs -df
Filesystem           Size     Used    Available  Use%
hdfs://shbHa  57936977920  6070272  52106985472    0%
```

## FS 내용 확인

```bash
[root@hdfsserver1 ~]# hadoop fs -ls /
Found 2 items
drwxrwxrwx   - root supergroup          0 2022-04-14 18:45 /tmp
drwxr-xr-x   - root supergroup          0 2022-04-14 19:08 /user
```

## WebPage를 이용하여 확인

```xml
<!– hdfs-site.xml -->
<!– dfs.namenode.http-address.shbHa.nn 에 설정한 포트 값 < 50070 >

http://localhost:50070/

```

![image](https://user-images.githubusercontent.com/53324492/168628684-7f230d36-a3ad-4d8e-8069-e4e7e81a945c.png)

## MapReduce 테스트

```bash
<!– Pi를 구하는 MapReduce 예제  -->

 /etc/hadoop/bin/yarn jar   /etc/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar pi 16 1000

```

위 **`/etc/hadoop/bin/yarn jar`**는 본인의 **`HADOOP_HOME/bin/yarn jar`**이다.

다음과 같이 수행되면 성공, 8089 (yarn-site.xml에서 설정함) 포트에서 확인할 수 있다.

![Mapreduce Example](https://user-images.githubusercontent.com/53324492/168629418-48e5732d-27c5-4382-9c47-42283774e4cf.png)
