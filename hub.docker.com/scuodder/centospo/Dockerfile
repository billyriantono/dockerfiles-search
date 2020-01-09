FROM consol/centos-xfce-vnc

ENV REFRESHED_AT 2018-03-18


# switching to root user to install wine 
USER 0


#RUN yum install epel-release && yum clean all

#RUN yum install wine -y && yum clean all
RUN yum -y install epel-release && rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm && yum clean all
RUN yum -y install obs-studio && yum clean all 


#REMOVE -rf /var/cache/yum


#switching back to some random user to disable root priviledges to make deployment process on openshift possible(refer openshift docs) 
USER 1000 





