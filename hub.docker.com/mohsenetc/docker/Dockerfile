FROM alpine:latest
#mohsen ahmadian < https://mohsenahmadian.info >

RUN mkdir -p /home/windows
RUN echo "Directory Created"
WORKDIR /home/windows

COPY bootstrap.sh /home/windows/bootstrap.sh
RUN chown root:root /home/windows/bootstrap.sh
RUN chmod 700 /home/windows/bootstrap.sh
ENV BOOTSTRAP /home/windows/bootstrap.sh

COPY . /home/windows

CMD ["./bootstrap.sh","-d"]
