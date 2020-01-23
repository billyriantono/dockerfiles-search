FROM dimkk/ant

MAINTAINER  dimkk

COPY . /var/l2

RUN ant -buildfile "/var/l2/l2game-filter.xml" build

WORKDIR /var/l2/

RUN chmod +x loop.sh

CMD ["sh", "loop.sh"]