# hadoop

实验准备环境

192.168.1.10    nn01      #namenode, secondary                 
192.168.1.11    node1     #datanode                 
192.168.1.12    node2     #datanode                     
192.168.1.13    node3     #datanode                                

192.168.1.15    nfsgw                            
192.168.1.20    nn02                                    
192.168.1.18    client                                             


每台主机：2G内存，2cpu，10G硬盘，1网卡                                   
设置主机名，和/ect/hosts                                         
配置yam                                     
准备好Hadoopo软件包              
https://pan.baidu.com/s/1zbBp9WGUrKBPdBCKDxWe_g                            
提取码：hrgn                                                                      

可ansible配置环境                                   

需要依赖包：java-1.8.0-openjdk-devel                               

官网下载软件包
将解压好的目录，cp到/usr/local/hadoop
                                                                                                            
配置ssh信任关系：
ansible  传递ssh-keygen   公钥
并且，在首次ssh时，不能出现询问yes的情况

对于配置文件，需要查看官方手册:http://hadoop.apache.org/docs/    ->  版本    -> 最下方左侧Configuration 项目中

修改配置文件：/usr/local/hadoop/etc/hadoop/hadoop-env.sh
export JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.131-11.b12.el7.x86_64/jre/"                   //指出jdk所在目录
export HADOOP_CONF_DIR="/usr/local/hadoop/etc/hadoop"             //指出hadoop配置文件所在位置

查看jdk所在目录方法：rpm -ql java-1.8.0-openjdk               //看所有的文件的公共路径

在/usr/local/hadoop/etc    下的core-site.xml   hdfs-site.xml                                
#<configuration>                            
#   <property>                                      
#      <name></name>                                   
#      <value></value>                              
#      <description></description>             //描述信息，可写可不写                                 
#   </property>                                   
#</configuration>                         
   
配置文件 slaves                            
里面添加所有作Datanode的主机名                           
   
      
查看版本命令： /usr/local/hadoop/bin/hadoop    version                     
对于hadoop的每台主机，配置文件都一样，故只需要配置好一台主机，然后scp 或ansible 传给其他主机                         





启动集群：                             
主机     动作                             
ALL：创建存储数据的目录，本实验是/var/hadoop     在core-site.xml里描述                              
node：拷贝hadoop的目录，本实验是/usr/local/hadoop                              
nn01： 格式化   /usr/local/hadoop/bin/hdfs   namenode   -format                                     
nn01: 启动集群：/usr/local/hadoop/sbin/start-dfs.sh
nn01: 启动yarn：/usr/local/hadoop/sbin/start-yarn.sh
nn01:启动全部：/usr/local/hadoop/sbin/start-all.sh
验证： all ： jps                                        
      nn01：  /usr/local/hadoop/bin/hdfs   dfsadmin  -report
      
      

web页面浏览
http://192.168.1.10:50070
http://192.168.1.10:50090
http://192.168.1.10:8088
http://192.168.1.11:50075
http://192.168.1.11:8042






