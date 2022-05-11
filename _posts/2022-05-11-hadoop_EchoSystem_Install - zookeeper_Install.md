---
layout: single
title: "CentOS7_zookeeper_Install"
categories: hadoopEchoSystem
tag: [Linux, Centos, Install, Hadoop, EcoSystem, zookeeper]
---

{% capture my_index %}{%include_relative index/hadoop_echosystem_install.md %}{% endcapture %}
{{ my_index | markdownify }}

---

# 다운로드 및 설치

필자는 회사에 구축되어 있는 것을 기준으로 구축을 재 구축을 해야해서 , 3.4.6 버전을 이용하여 설치를 진행했다

각자 원하는 버전을 이용하여 설치하면 될 것 같다.

[공식 아파치 아카이브](https://archive.apache.org/dist/zookeeper) 이곳에 들어가서 원하는 경로에 맞게 설치해주면 된다.

```bash
wget https://archive.apache.org/dist/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz
# 만약 원하는 설치 경로가 존재한다면 -C 옵션을 이용하여 해당 경로로 압축 해제를 해도 된다.
tar xvfz zookeeper-3.4.6.tar.gz
```

# zoo.CFG 설정

압축 해제한 zoo.cfg 파일을 본인에게 맞게 설정해 주면된다.

필자는 Host설정을 해서 ip 주소가 아닌 HOST정보로 작성 및 HA구성을 하였다.

```conf
clientPort=2181
initLimit=10
autopurge.purgeInterval=24
syncLimit=5
tickTime=3000
<!– Zookeeper에서 산출되는 데이터를 저장할 위치, 추후 에러 등이 발생하면 들어가볼 경로라 생각하면 된다. -->
dataDir=/hadoop/zookeeper
autopurge.snapRetainCount=30
<!– /etc/hosts 에서 설정-->
<!– 2888 : Input-->
<!– 2888 : output-->
server.1=hdfsserver1.com:2888:3888
server.2=hdfsserver2.com:2888:3888
server.3=hdfsserver3.com:2888:3888
```

vim으로 작성하기 귀찮다면, 아래와 같이 cat명령어를 이용하여 작성해도 된다.

```bash
# 본인의 zoo.cfg파일 경로
cat > /etc/zookeeper/conf/zoo.cfg << EOF
clientPort=2181
initLimit=10
autopurge.purgeInterval=24
syncLimit=5
tickTime=3000
dataDir=/hadoop/zookeeper
autopurge.snapRetainCount=30
server.1=hdfsserver1.com:2888:3888
server.2=hdfsserver2.com:2888:3888
server.3=hdfsserver3.com:2888:3888
EOF
```

위와 같이 설정하고 가장 먼저 해 줘야할
dataDir로 지정한 데이터 경로에 해당하는 server.N의 값이 **myid**로 저장되어 있어야 한다.

> 만약 server.1 이라면, vim, cat 등을 이용하여 해당 경로에 1이 들어있는 myid 파일을 생성해주면 된다.
>
> ```bash
> cat /hadoop/zookeeper/myid << EOF
> 1
> EOF
> ```

# 실행

```bash
<!– Zookeeper 실행-->
zkServer.sh start

<!– Zookeeper 종료-->
zkServer.sh stop

```

# 테스트

아래 테트는 각 1,2,3 번에 들어가서 테스트를 해봐야한다.

```bash
<!– CLI를 통해 서버 접속-->
    bin/zkCli.sh –server 127.0.0.1:2181

<!– Zookeeper 생성 / 조회 / 삭제 테스트-->

    create /zk_znode_1 sample_data

    get /zk_znode_1

   delete /zk_znode_1


```

다음과 같이 모든 노드가 아래와 같다면 성공한 것이다.

![zookeeper Test 성공 이미지](https://user-images.githubusercontent.com/53324492/167885638-805a1bd3-cd03-4697-9881-cf463270d300.png)

**`myid, hosts(ip), 포트포워딩`** 만 잘 작성하면 쉽게 구현할 수 있다. 화이팅!
