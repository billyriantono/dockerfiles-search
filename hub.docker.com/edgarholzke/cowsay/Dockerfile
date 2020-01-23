FROM debian

MAINTAINER Edgar Holzke <edgar.holzke@gmail.com>
RUN apt-get update && apt-get install -y cowsay fortune fortune-mod fortunes fortunes-de

RUN echo "de_DE.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "de_DE ISO-8859-1" >> /etc/locale.gen
RUN echo "de_DE@euro ISO-8859-15" >> /etc/locale.gen

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

