FROM store/oracle/database-instantclient:12.2.0.1
ADD sqld* .
 RUN yum -y install tar* gcc* gcc-c++ unzip zip  openssh* libaio* make curl \
	&& unzip sqld360*.zip \
	&& yum clean all

