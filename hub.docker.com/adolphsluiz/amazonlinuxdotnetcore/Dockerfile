FROM amazonlinux

RUN /bin/bash -c 'yum install libunwind libicu libuuid -y'
RUN /bin/bash -c 'curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?LinkID=835019'
RUN /bin/bash -c 'mkdir -p /opt/dotnet && tar zxf dotnet.tar.gz -C /opt/dotnet'
RUN /bin/bash -c 'ln -s /opt/dotnet/dotnet /usr/local/bin'
