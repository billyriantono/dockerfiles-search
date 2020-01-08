FROM drydock/u16:v5.10.4

ADD . /u16dotnet

RUN /u16dotnet/install.sh && rm -rf /tmp && mkdir /tmp && chmod 1777 /tmp
