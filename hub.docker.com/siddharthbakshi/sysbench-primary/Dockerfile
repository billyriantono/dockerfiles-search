FROM centos:7
MAINTAINER Siddharth Bakshi

RUN yum -y install epel-release
RUN yum -y install libcgroup
# RUN yum -y install gcc openssl-devel bzip2-devel
# RUN cd /usr/src
# RUN wget https://www.python.org/ftp/python/3.6.8/Python-3.6.8.tgz
# RUN tar xzf Python-3.6.8.tgz
# RUN cd Python-3.6.8
# RUN ./configure --enable-optimizations
# RUN make altinstall
# RUN rm /usr/src/Python-3.6.8.tgz
RUN yum -y install python-pip
RUN pip install --upgrade pip
RUN yum -y install gcc python2-devel
RUN pip install --upgrade setuptools
RUN pip install psutil
# RUN yum -y install make
RUN yum -y install sysbench
RUN yum -y clean all
# RUN chmod -R 777 /root/
# RUN chmod -R 777 /var/
# RUN chmod -R 777 /home/
# RUN chmod -R 777 /etc/
# RUN chmod -R 777 /usr/
# RUN chmod -R 777 /bin/
# RUN chmod -R 777 /lib/
# RUN chmod -R 777 /sbin/
# RUN for ID in $(cat /etc/passwd | grep /home | cut -d ':' -f1);  do adduser $ID boinc;done
# RUN chmod 777 /var/lib/boinc/
# RUN chmod 777 /var/lib/boinc/*.*
#RUN free_mem=$(free | sed -n 's/^Mem:\s\+[0-9]\+\s\+[0-9]\+\s\+\([0-9]\+\)\s.\+/\1/p')
#RUN echo $free_mem
#free_mem=$(free | sed -n 's/^Mem:\s\+[0-9]\+\s\+[0-9]\+\s\+\([0-9]\+\)\s.\+/\1/p')
#expr 100 \* 140 / 200 - 20
#RUN echo hello_world >foo.txt
#RUN chmod 777 /sys/fs/cgroup

#grep 'cpu ' /proc/stat | awk '{usage=($2+$4)*100/($2+$4+$5)} END {print usage "%"}'
#echo $( cut -d ',' -f 2 <<< "$(id)")

# ENV boincurl www.worldcommunitygrid.org
# ENV boinckey 0306042ebf9cb4311fef19de74b91a2e

CMD sysbench --test=cpu --cpu-max-prime=900000000000000000000 run
