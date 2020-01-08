
#Instalación sistema operativo Centos 7
FROM centos:7
#Ejecución de los comandos como root
USER root
#Instalación del wget para descargar recursos via curl y del ssh server
RUN yum install wget -y
RUN yum clean all; \
    rpm --rebuilddb; \
    yum install -y curl which tar sudo openssh-server openssh-clients rsync
#Instalación de paquetes
RUN yum update -y libselinux
RUN yum install -y net-tools
RUN yum install -y vim
RUN yum install -y telnet
#Generación de authorized_keys para la comunicación entre nodos
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa
RUN cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys
#configuración y permisos del shh con el usuario root
ADD ssh_config /root/.ssh/config
RUN chmod 600 /root/.ssh/config
RUN chown root:root /root/.ssh/config
#CONFIGURACIÓN DE HADOOP
#Iniciamos la descarga con el wget desde el repositorio de apache para hadoop version 3
RUN cd ~ && wget http://www-eu.apache.org/dist/hadoop/common/hadoop-3.2.0/hadoop-3.2.0.tar.gz
#Añadimos el paquete rpm del JDK de Java
ADD ./jdk-8u211-linux-x64.rpm /jdk-8u211-linux-x64.rpm
RUN cd /
RUN rpm -Uvh jdk-8u211-linux-x64.rpm
#Descompreción de archivos Hadoop en directorio /opt
RUN cd /opt/
RUN cd ~ && tar xvf hadoop-3.2.0.tar.gz -C /opt
#Configuración del fichero env de Hadoop
ADD ./hadoop-env.sh /hadoop-env.sh
RUN cp /hadoop-env.sh /opt/hadoop-3.2.0/etc/hadoop/hadoop-env.sh
#Creación de directorio para los metadatos de HDFS
RUN cd /
RUN mkdir datos && cd datos && mkdir namenode && cd
#Copia de los ficheros configurados en el directorio /etc/hadoop
ADD ./core-site.xml /core-site.xml
RUN cp /core-site.xml /opt/hadoop-3.2.0/etc/hadoop/core-site.xml
ADD ./hdfs-site.xml /hdfs-site.xml
RUN cp /hdfs-site.xml /opt/hadoop-3.2.0/etc/hadoop/hdfs-site.xml
ADD ./mapred-site.xml /mapred-site.xml
RUN cp /mapred-site.xml /opt/hadoop-3.2.0/etc/hadoop/mapred-site.xml
ADD ./yarn-site.xml /yarn-site.xml
RUN cp /yarn-site.xml /opt/hadoop-3.2.0/etc/hadoop/yarn-site.xml
ADD ./workers /workers
RUN cp /workers /opt/hadoop-3.2.0/etc/hadoop/workers
#Definición de las variables de entorno necesarias para la ejecución de binarios
ENV HADOOP_HOME=/opt/hadoop-3.2.0
ENV JAVA_HOME=/usr/java/jdk1.8.0_211-amd64
ENV HDFS_NAMENODE_USER="root"
ENV HDFS_DATANODE_USER="root"
ENV HDFS_SECONDARYNAMENODE_USER="root"
ENV YARN_RESOURCEMANAGER_USER="root"
ENV YARN_NODEMANAGER_USER="root"
ENV HADOOP_COMMON_HOME /opt/hadoop-3.2.0
ENV HADOOP_HDFS_HOME /opt/hadoop-3.2.0
ENV HADOOP_MAPRED_HOME /opt/hadoop-3.2.0
ENV HADOOP_YARN_HOME /opt/hadoop-3.2.0
ENV HADOOP_CONF_DIR /opt/hadoop-3.2.0/etc/hadoop
#Permisos directorios de configuración Hadoop
RUN ls -la /opt/hadoop-3.2.0/etc/hadoop/*-env.sh
RUN chmod +x /opt/hadoop-3.2.0/etc/hadoop/*-env.sh
RUN ls -la /opt/hadoop-3.2.0/etc/hadoop/*-env.sh
#Configuración adicional del ssh para evitar errores
RUN sed  -i "/^[^#]*UsePAM/ s/.*/#&/"  /etc/ssh/sshd_config
RUN echo "UsePAM no" >> /etc/ssh/sshd_config
RUN echo "Port 2122" >> /etc/ssh/sshd_config
#Copia del archivo hosts y authorized_keys para comunicación de red entre Nodos
ADD ./hosts /hosts
COPY ./hosts /etc/hosts
ADD ./authorized_keys /authorized_keys
RUN cp /authorized_keys /root/.ssh/authorized_keys
#Puertos Hadoop HDFS
EXPOSE 9866 9864 9865 9867 8111 50071 50072 888 8480 8481 8485 50100 50105 9870 9871 9868 9869 50200 9000
#Puertos YARN
EXPOSE 2181 10020 10033 19888 19890 8049 8048 8040 8042 8044 8032 8033 8031 8030 8088 8090 8089 8091 8047 8045 8046 8788 10200 8188 8190
#---------------------------------------------------------------------------------------------------------
#----------------------------------------HIVE-------------------------------------------------------------
#Descarga paquete Hive desde apache.org
RUN cd ~ &&  wget https://www-eu.apache.org/dist/hive/hive-3.1.1/apache-hive-3.1.1-bin.tar.gz
RUN cd ~ && tar xvf apache-hive-3.1.1-bin.tar.gz -C /opt
RUN cd /opt && mv apache-hive-3.1.1-bin/ hive
#Variable de entorno de Hive
ENV HIVE_HOME=/opt/hive
#Path de las variables de entorno
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:/usr/java/jdk1.8.0_211-amd64/bin:$HIVE_HOME/bin
#Copia de los ficheros de configuración de hive
COPY /hive-site.xml /opt/hive/conf/
COPY /hive-env.sh /opt/hive/conf/
COPY /beeline-log4j2.properties /opt/hive/conf/
COPY /hive-exec-log4j2.properties /opt/hive/conf/
COPY /hive-log4j2.properties /opt/hive/conf/
#Se exponen los puertos necesarios para el hiveserver2
EXPOSE 10000 9083 10001 10002
#Creación de carpetas donde se almacenara la Base de datos en HDFS
#RUN hdfs dfs -mkdir /tmp
#RUN hdfs dfs -chmod g+w /tmp
#RUN hdfs dfs -mkdir -p /user/hive/warehouse
#RUN hdfs dfs -chmod g+w /user/hive/warehouse
#Creación de directorio donde se almacenará metadatos de configuración
RUN cd /opt/hive && mkdir bbdd
#inicialización de la base de datos tipo Derby
#RUN schematool -dbType derby -initSchema
#Iniciación del servidor Hive para conexiones remotas por cliente OBDC
#RUN hiveserver2 &

#RUN hdfs namenode -format
#RUN hdfs --daemon start namenode
#RUN hdfs --daemon start secondarynamenode
#---------------------------------------------------------------------------------------------------------
#----------------------------------------HUE-------------------------------------------------------------
RUN yum install libffi-devel -y
RUN yum install gmp-devel -y
RUN yum install python-devel mysql-devel -y
RUN yum install ant gcc gcc-c++ rsync krb5-devel mysql openssl-devel cyrus-sasl-devel cyrus-sasl-gssapi sqlite-devel openldap-devel python-simplejson -y
RUN yum install libtidy libxml2-devel libxslt-devel -y
RUN yum install python-devel python-simplejson python-setuptools -y
RUN yum install maven -y
RUN yum install make -y
COPY /hue-4.4.0 /opt/hue
RUN cd /opt/hue && ls && PREFIX=/opt/hadoop-3.2.0 make install
RUN cd /opt/hadoop-3.2.0/hue/desktop/conf
ADD ./hue.ini /hue.ini
COPY /hue.ini /opt/hadoop-3.2.0/hue/desktop/conf
RUN adduser hue
RUN chown -R hue:hue /opt/hadoop-3.2.0/hue/
#RUN cd /opt/hadoop-3.2.0/hue/build/env/bin/supervisor -d
EXPOSE 8888 8983
ADD ./script.sh /script.sh
ADD ./stop.sh /stop.sh
