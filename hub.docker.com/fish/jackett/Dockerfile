FROM mono:5.18

ENV VERSION=v0.10.890
ENV URL=https://github.com/Jackett/Jackett/releases/download/${VERSION}/Jackett.Binaries.Mono.tar.gz

RUN curl -Lsf "$URL" | tar -C /opt -xzf -

RUN useradd user && install -d -o user -g user /data
USER user
VOLUME /data

EXPOSE 9117
ENTRYPOINT [ "mono", "/opt/Jackett/JackettConsole.exe", "--DataFolder=/data" ]
