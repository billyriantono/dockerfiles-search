#Simple ENV test
FROM centos
LABEL maintainer "csweet"

ENV ENV_PHRASE=HELLO
ENV CUSTOM_PHRASE=lololol

WORKDIR /usr/bin/
COPY run.sh .
RUN chmod u+x run.sh

CMD bash ./run.sh