FROM nskalski/alpine-python3
RUN ["pip", "install", "--no-cache-dir", "Django"]
RUN ["rm", "-rf", "/var/cache/*"]
RUN ["rm", "-rf", "/root/.cache/*"]

EXPOSE 8000/tcp
