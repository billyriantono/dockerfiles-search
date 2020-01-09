FROM centos:7
MAINTAINER "digitman5509" <den5509@mail.ru>
ENV container docker
#
# Обновление и очистка
RUN yum -y update; yum clean all;
#
# Установка пакетов необходимых для выполнения лабораторной работы
RUN yum -y install make nano gcc git sudo; yum clean all;
#
# файлы для выполнение лабораторной работы внутри контейнера
ADD . /home/lab4
#
# скрипт, выводящий на экран отчет и запускающий bash
# при запуске контейнера
CMD ["/home/lab4/init"]
#
# Порт для проброса на хост
EXPOSE 80
