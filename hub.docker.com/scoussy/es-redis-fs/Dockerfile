FROM alpine

COPY . /src
RUN chmod 755 /src/build.sh 
RUN /src/build.sh

ADD ./entrypoint.sh /entrypoint.sh
RUN chmod 755 /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]
