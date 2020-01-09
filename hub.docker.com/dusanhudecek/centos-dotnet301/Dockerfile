FROM registry.centos.org/centos:latest

RUN yum -y install wget curl unzip dos2unix rpm-build rpmdevtools git openssh-clients epel-release https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm && \
    yum -y install dotnet-sdk-3.0