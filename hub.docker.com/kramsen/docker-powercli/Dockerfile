FROM centos:latest
MAINTAINER matthias-brueckner@live.de

RUN yum -y install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-alpha.14/powershell-6.0.0_alpha.14-1.el7.centos.x86_64.rpm \
                   ftp://ftp.pbone.net/mirror/ftp5.gwdg.de/pub/opensuse/repositories/home:/Scott_Cantor/CentOS_7/x86_64/libcurl-openssl-7.43.0-1.1.x86_64.rpm \
                   unzip

RUN curl -sSL -o PowerCLI_Core.zip https://download3.vmware.com/software/vmw-tools/powerclicore/PowerCLI_Core.zip
RUN mkdir -p ~/.local/share/powershell/Modules
RUN unzip PowerCLI_Core.zip && unzip 'PowerCLI.*.zip' -d ~/.local/share/powershell/Modules
RUN mv /opt/shibboleth/lib64/libcurl.so.4.3.0 /usr/lib64


#COPY entrypoint.sh /sbin/entrypoint.sh
#RUN chmod 755 /sbin/entrypoint.sh

ENTRYPOINT ["/bin/bash"]
