FROM python:3

# RUN apk add --no-cache --upgrade bash
# RUN apk add --no-cache openssh-client
# RUN apk add --no-cache build-base

RUN apt-get install openssh-client -y

RUN pip install --no-cache python-openstackclient

WORKDIR /root

COPY execute.sh .
RUN chmod 744 execute.sh

COPY remote_host_execute.sh .
RUN chmod 744 remote_host_execute.sh

COPY backup.sh .
RUN chmod 744 backup.sh

COPY scp_tarball.sh .
RUN chmod 744 scp_tarball.sh

COPY upload_to_swift.sh .
RUN chmod 744 upload_to_swift.sh

CMD ./execute.sh