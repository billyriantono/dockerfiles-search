FROM alpine
RUN ["apk", "upgrade", "--no-cache"]
RUN ["apk", "add", "--no-cache", "python3", "python3-dev", "git", "vim"]
RUN ["pip3", "install", "--no-cache-dir", "--upgrade", "pip"]
RUN ["rm", "-rf", "/var/cache/*"]
RUN ["rm", "-rf", "/root/.cache/*"]

WORKDIR /usr/bin
RUN ["ln", "-sf", "python3", "python"]
RUN ["ln", "-sf", "pip3", "pip"]

WORKDIR /
