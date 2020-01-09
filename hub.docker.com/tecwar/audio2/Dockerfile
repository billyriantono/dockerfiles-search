FROM        ubuntu:xenial

LABEL       author="srkhost" maintainer="bereczkimzoltan@gmail.com"

RUN         apt-get update \
            && apt-get upgrade -y \
            && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
            && apt-get install -y apt-transport-https \
            && echo "deb https://download.mono-project.com/repo/ubuntu stable-xenial main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
            && apt-get update \
            && apt -y --no-install-recommends install ffmpeg wget zip youtube-dl unzip libopus-dev python mono-complete \
            && useradd -d /home/container -m container


USER        container
ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh

CMD         ["/bin/bash", "/entrypoint.sh"]
