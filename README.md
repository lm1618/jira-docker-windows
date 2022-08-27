

For Windows 教程

文件下载：
安装包：https://www.atlassian.com/zh/software/jira/update

激活文件：https://github.com/haxqer/jira  

JDK8（可以不安装，Jira内置）   https://545c.com/dir/15405323-40806633-3e407b

数据库推荐使用：https://www.postgresql.org/  配置比MySQL较简单

官方帮助文件：
https://confluence.atlassian.com/adminjiraserver/installing-jira-applications-on-windows-938846835.html#

参考
https://github.com/keygood/atlassian-agent
https://github.com/hgqapp/atlassian-agent

1.安装postgresql并创建数据库，使用pgAdmin创建数据库jira 用户jira 密码jira，添加用户jira权限，用户名密码可自己修改，后续配置也需用到
![image](https://user-images.githubusercontent.com/63717679/187026128-a3e48b39-74e7-4e6d-aabd-76c37cf43d73.png)
![image](https://user-images.githubusercontent.com/63717679/187026154-d37a4525-0e59-4392-a4ae-a6e70c44dfb7.png)
![image](https://user-images.githubusercontent.com/63717679/187026177-2bef03af-c741-484b-98e0-08a8fb87d4d7.png)

2.安装Jira，勾选安装为 Windows Service，并按照要求配置数据库postgresql localhost 端口号  数据库：jira 用户：jira 密码：jira，到激活界面关闭Jira，使用开始菜单中的“Stop Jira Service [8080]”

3.激活
  将atlassian-agent.jar放在无空格的英文路径下，
  修改Atlassian Jira服务，使用SrvanyUI修改 自行下载，启动参数后加 ++JvmOptions=-javaagent:E:\Atlassian\atlassian-agent.jar  注意atlassian-agent.jar路径
  
  ![image](https://user-images.githubusercontent.com/63717679/187027481-763a47cc-f6ea-42e0-b285-9b08e330abbe.png)

    开始菜单中的“Start Jira Service [8080]”启动Jira
   
   激活码生成，如果没有安装jdk，需要使用C:\Program Files\Atlassian\Jira\jre\bin 目录下的java执行，cmd切换到该目录运行。

    java -jar E:\Atlassian\atlassian-agent.jar -p jira -m haxqer666@gmail.com -n haxqer666@gmail.com -o http://website -s 用户ID

   
   激活插件程序

   java -jar E:\Atlassian\atlassian-agent.jar  -p eu.softwareplant.biggantt(插件名称) -m haxqer666@gmail.com -n haxqer666@gmail.com -o http://website -s 用户ID
   
   可以运行 java -jar E:\Atlassian\atlassian-agent.jar  查看相关帮助
   
   
   [![docker pulls](https://img.shields.io/docker/pulls/haxqer/jira.svg)](https://hub.docker.com/r/haxqer/jira/)  [![docker stars](https://img.shields.io/docker/stars/haxqer/jira.svg)](https://hub.docker.com/r/haxqer/jira/) [![image metadata](https://images.microbadger.com/badges/image/haxqer/jira.svg)](https://microbadger.com/images/haxqer/jira "haxqer/jira image metadata")

[kubernetes helm charts](https://github.com/haxqer/charts)

# jira
default port: 8080

## requirement
- docker: 17.09.0+
- docker-compose: 1.24.0+

## How to run with docker-compose

- start jira & mysql

```
    git clone https://github.com/haxqer/jira.git \
        && cd jira \
        && git checkout rm \
        && docker-compose pull \
        && docker-compose up
```

- start jira & mysql daemon

```
    docker-compose up -d
```

- default db(mysql5.7) configure:

```bash
    driver=mysql5.7+
    host=mysql-jira
    port=3306
    db=jira
    user=jira
    passwd=123123
```

## How to run with docker

- start jira

```
    docker run -p 8080:8080 -v jira_home_data:/var/jira --network jira-network --name jira-srv -e TZ='Asia/Shanghai' haxqer/jira:rm
```

- config your own db:


## How to hack jira

```
docker exec jira-srv java -jar /var/agent/atlassian-agent.jar \
    -p jira \
    -m haxqer666@gmail.com \
    -n haxqer666@gmail.com \
    -o http://website \
    -s you-server-id-xxxx
```

## How to hack jira plugin

- .eg I want to use BigGantt plugin
1. Install BigGantt from jira marketplace.
2. Find `App Key` of BigGantt is : `eu.softwareplant.biggantt`
3. Execute :

```
docker exec jira-srv java -jar /var/agent/atlassian-agent.jar \
    -p eu.softwareplant.biggantt \
    -m haxqer666@gmail.com \
    -n haxqer666@gmail.com \
    -o http://website \
    -s you-server-id-xxxx
```

4. Paste your license 

## Install docker & docker-compose
- If you use `debian`, just do it.
```
    ./script/debian-install-docker.sh
    ./script/linux-install-docker-compose.sh
```

## Set Proxy

path : `~/.docker/config.json`

content : 
```
{
    "proxies": {
        "default": {
         "httpProxy": "http://ip:port",
         "httpsProxy": "http://ip:port"
        }
    }
}
```
