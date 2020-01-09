FROM alpine:3.7
MAINTAINER jack <jackadam@sina.com> 
#echo 'https://mirrors.tuna.tsinghua.edu.cn/alpine/v3.7/community/'>/etc/apk/repositories  && \
#echo 'https://mirrors.tuna.tsinghua.edu.cn/alpine/v3.7/main/'>>/etc/apk/repositories  && \
RUN apk add --no-cache samba-common-tools samba-server tzdata &&\
	echo '[global]' >/etc/samba/smb.conf && \
	echo 'netbios name = Samba' >>/etc/samba/smb.conf && \
	echo 'workgroup = WORKGROUP' >>/etc/samba/smb.conf && \
	echo 'server string = Samba Server' >>/etc/samba/smb.conf && \
	echo 'map to guest = bad user' >>/etc/samba/smb.conf && \
	echo 'browsenable = yes' >>/etc/samba/smb.conf && \
	echo '[share]' >>/etc/samba/smb.conf && \
	echo 'path = /share' >>/etc/samba/smb.conf && \
	echo 'public = yes ' >>/etc/samba/smb.conf && \
	echo 'writable = yes' >>/etc/samba/smb.conf && \
	echo 'create mask = 0765' >>/etc/samba/smb.conf && \
	rm -rf /tmp/* && \
	cp /usr/share/zoneinfo/Asia/Chongqing /etc/localtime

EXPOSE 137/udp \
       138/udp \
       139/tcp \
       445/tcp

CMD nmbd -D && smbd -FS