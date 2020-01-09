FROM mcr.microsoft.com/powershell

RUN apt-get update && apt-get install -y \
    curl \
    file 
#RUN apt-get install -y python3-pip  || true
#RUN apt-get install -y python2-pip || true
RUN apt-get install -y python-pip || true

# Install GoVC
RUN curl -s -L -o /tmp/govc.gz "https://github.com/vmware/govmomi/releases/download/v0.21.0/govc_linux_amd64.gz" && gzip -d /tmp/govc.gz && mv /tmp/govc /usr/bin/govc && chmod ugo+x /usr/bin/govc

# Install & prepare PowerCli
COPY install_powercli_repo.ps1 /root/
RUN pwsh /root/install_powercli_repo.ps1
COPY install_powercli_module.ps1 /root/
RUN pwsh /root/install_powercli_module.ps1
COPY install_powercli_defaults.ps1 /root/
RUN pwsh /root/install_powercli_defaults.ps1
COPY install_powercli_testing.ps1 /root/
RUN pwsh /root/install_powercli_testing.ps1

# Install & prepare Python on steroids
RUN pip install --upgrade pyvmomi || true
RUN pip install --upgrade ansible || true
RUN pip install --upgrade influxdb || true
RUN pip install --upgrade sqlalchemy  || true
#RUN pip3 install --upgrade pyvmomi || true
#RUN pip3 install --upgrade ansible || true
#RUN pip3 install --upgrade influxdb || true
#RUN pip3 install --upgrade sqlalchemy  || true
