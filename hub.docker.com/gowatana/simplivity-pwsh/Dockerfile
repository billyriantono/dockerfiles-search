FROM centos

LABEL maintainer="gowatana" \
      version="0.1"
      
# Install PowerShell
RUN curl -o /etc/yum.repos.d/ms.repo https://packages.microsoft.com/config/rhel/7/prod.repo
RUN yum install -y powershell-6.0.4

# Set Working directory.
WORKDIR /work

# Set SimpliVity API script sample.
RUN mkdir -p ~/.config/powershell && \
    curl -o ~/.config/powershell/profile.ps1 https://raw.githubusercontent.com/gowatana/svt-powershell-sample/master/SVT_PowerShell_Samples.ps1

RUN yum clean all

CMD ["/bin/pwsh","-NoLogo"]
