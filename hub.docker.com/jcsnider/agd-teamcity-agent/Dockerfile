FROM jetbrains/teamcity-agent

RUN apt-get update && \
    apt-get install -y nodejs npm
    
RUN apt install gnupg ca-certificates -y && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list && \
    apt update && \
    apt install mono-devel -y
    
RUN apt install msbuild -y && \
    apt install nuget -y
