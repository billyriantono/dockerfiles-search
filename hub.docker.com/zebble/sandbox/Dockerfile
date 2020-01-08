FROM centos:latest
RUN yum -y upgrade
RUN yum -y install https://cdn.cloudbackup.management/maxdownloads/mxb-linux-1.x86_64.rpm
#RUN ln -s /opt/MXB/lib/libvixMntapi.so.1 /usr/lib64/
#RUN ln -s /opt/MXB/lib/libvixDiskLib.so.5 /usr/lib64/
#RUN ln -s /opt/MXB/lib/libfuse.so.2 /usr/lib64/
#RUN mkdir /host_data
ENTRYPOINT ["/bin/bash","-c","/opt/MXB/bin/ProcessController serve && /usr/bin/sleep 99999999999999"]
