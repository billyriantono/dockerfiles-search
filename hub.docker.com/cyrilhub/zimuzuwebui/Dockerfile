FROM centos
MAINTAINER Cyril Chan <cxhforever@gmail.com>
RUN mkdir /home/soft/ \
&& cd /home/soft/ \
&& yum install wget -y \
&& wget  -O rarlinux.tar.gz  http://cyril-c.cn/wp-content/uploads/2018/11/rarlinux-x64-5.3.0.tar.gz \
&& wget -O rrshareweb_linux.rar http://appdown.rrys.tv/rrshareweb_linux.rar \
&& tar -zxvf /home/soft/rarlinux.tar.gz  \
&& mkdir -p /usr/local/bin \
&& mkdir -p /usr/local/lib \
&& cp /home/soft/rar/rar /home/soft/rar/unrar /usr/local/bin \
&& cp /home/soft/rar/rarfiles.lst /etc \
&& cp /home/soft/rar/default.sfx /usr/local/lib \
&& unrar x rrshareweb_linux.rar \
&& tar -xvf rrshareweb_centos7.tar.gz \
&& mkdir /home/app \
&& cp /home/soft/rrshareweb /home/app -r \
&& mkdir -p /home/video \
&& mkdir -p /home/app/log \
&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  
COPY rrshare.json rrshare.db /home/app/rrshareweb/conf/
# ENTRYPOINT ["/home/app/rrshareweb/rrshareweb"]
CMD ["/home/app/rrshareweb/rrshareweb"]