FROM jupyter/minimal-notebook

USER root

RUN apt-get update && apt-get install -y gnupg curl \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
    && echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
    && curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - \
    && wget "https://github.com/PowerShell/PowerShell/releases/download/v6.1.0-preview.3/powershell-preview_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb" -O /tmp/psh.deb \
    && dpkg -i /tmp/psh.deb; apt-get install -fy \
    && apt-get update && apt-get install -y \
        mono-runtime \
        fsharp \
        htop \
        nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/* \
    && ln -s /opt/microsoft/powershell/6-preview/pwsh /usr/bin/

USER $NB_UID
# Install the F# Kernel
RUN mkdir /home/jovyan/ifs
WORKDIR /home/jovyan/ifs
RUN wget "https://github.com/fsprojects/IfSharp/releases/download/v3.0.0-beta3/IfSharp.v3.0.0-beta3.zip" -O ifsharp.zip \
    && unzip ifsharp.zip && rm ifsharp.zip \
    && mono ifsharp.exe
WORKDIR /home/jovyan
RUN npm install -g ijavascript && ijsinstall # Install Javascript (Node.js) Kernel
RUN pip install powershell_kernel && python -m powershell_kernel.install # Install Powershell Kernel
RUN mkdir ~/notebooks
WORKDIR /home/jovyan/notebooks
