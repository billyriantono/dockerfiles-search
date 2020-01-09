FROM debian:stable
MAINTAINER Aleksey Yaroslavcev <a.yaroslavcev@gmail.com>

#Îáíîâëåíèå ñïèñêà ïàêåòîâ
RUN apt-get update

#Óñòàíîâêà AStyle èç ðåïîçèòîðèÿ debian
RUN apt-get -y install astyle

#Î÷èñòêà êýøà ñêà÷åííûõ ïàêåòîâ
RUN apt-get -y clean;apt-get -y autoclean

#Êîïèðîâàíèå íàñòðîåê äëÿ ñòàéëåðà
COPY planar.astylerc /