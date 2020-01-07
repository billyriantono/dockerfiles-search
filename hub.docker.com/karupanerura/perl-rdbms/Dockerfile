FROM perl:5.30
LABEL maintainer="karupanerura <karupa@cpan.org>"

RUN apt update && env PATH="/usr/bin:$PATH" apt install -y postgresql mysql-server

WORKDIR /root

CMD ["perl5.30.0","-de0"]