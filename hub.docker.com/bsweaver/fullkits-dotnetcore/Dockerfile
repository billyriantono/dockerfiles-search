FROM consol/ubuntu-xfce-vnc
LABEL author=bryanweaver@outlook.com
ENV REFRESHED_AT 2018-02-07

USER 0

RUN apt-get -y update && apt-get -y install curl && apt-get -y install git-all && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

# Install dotnet core
RUN sh -c 'echo "deb [arch=amd64] http://packages.microsoft.com/repos/microsoft-ubuntu-xenial-prod xenial main" > /etc/apt/sources.list.d/dotnetdev.list' && \
    apt-get -y update && \
    apt-get -y install apt-transport-https && \
    apt-get -y install dotnet-sdk-2.1.4

# Install VS Code
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list' && \
    apt-get -y update && \
    apt-get -y install code && \
    apt-get -y autoremove && rm -f $HOME/.config/bg_sakuli.png

USER 1984

# Install VS Code extensions
RUN code --install-extension  ms-vscode.csharp

