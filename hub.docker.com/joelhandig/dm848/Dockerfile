FROM jolielang/jolie:latest


RUN apk update
RUN apk add git
RUN apk add bash

RUN git clone https://Joelhandig@bitbucket.org/Joelhandig/dm848.git

WORKDIR dm848

RUN java -version

RUN ls
RUN bash compile.sh

CMD ["jolie", "SubstringServer.ol"]

