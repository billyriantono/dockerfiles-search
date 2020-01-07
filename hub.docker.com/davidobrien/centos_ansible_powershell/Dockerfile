FROM centos:latest

RUN yum check-update; yum install -y gcc libffi-devel python-devel openssl-devel epel-release
RUN yum install -y python-pip python-wheel

RUN pip install ansible[azure]

# Change this URL to the exact version you want to install
ENV POWERSHELL_DOWNLOAD_URL https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm

RUN curl -L $POWERSHELL_DOWNLOAD_URL --output powershell_linux.rpm; yum -y install powershell_linux.rpm ; rm powershell_linux.rpm --force
RUN yum clean packages; yum clean all