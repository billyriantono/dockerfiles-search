FROM centos:latest
RUN rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm \
  && yum update -y && yum install -y libunwind libicu dotnet-runtime-2.1.0 wget rsync \
  && yum clean all \
  && wget -O /tmp/azcopy.tar.gz https://aka.ms/downloadazcopylinux64 \
  && tar -xf /tmp/azcopy.tar.gz -C /tmp \
  && /tmp/install.sh \
  && rm -rf /tmp/azcopy.tar.gz /tmp/azcopy /tmp/install.sh