FROM mysql
MAINTAINER Raenko Ivan <admin@sysadminsk.ru>

ENV LANG=ru_RU.utf8 \
 LC_ALL=ru_RU.utf8 \
 LANGUAGE=ru_RU.utf8 \
 TZ=Asia/Novosibirsk

RUN apt -y update && apt -y install locales && localedef -i ru_RU -f UTF-8 ru_RU.UTF-8
