FROM mongo:4.0
LABEL maintainer="hajo@ventx.de"

RUN apt-get update && apt-get install git openssh-client unzip zip -y

CMD ["mongo", "--version"]
