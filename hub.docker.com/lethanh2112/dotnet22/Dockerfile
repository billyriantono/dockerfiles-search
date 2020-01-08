FROM centos:centos7
MAINTAINER thanhcl <thanhcl@vsit.com.vn>

USER root
RUN rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
RUN yum update -y
RUN yum install dotnet-sdk-2.2 -y
USER ${user}

