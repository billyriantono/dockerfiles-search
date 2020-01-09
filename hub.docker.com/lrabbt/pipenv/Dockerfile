FROM python:2.7

MAINTAINER Breno <lrabbt@gmail.com>

WORKDIR /app

# Update pip
RUN ["pip", "install", "--upgrade", "pip"]

# Install PipEnv and bottle
RUN ["pip", "install", "pipenv"]

# Adding run script and Bottle PipFile
COPY run.sh /
RUN ["chmod", "+x", "/run.sh"]

VOLUME /app

EXPOSE 8080

CMD ["sh", "/run.sh"]
