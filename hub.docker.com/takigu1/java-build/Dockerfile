FROM ubuntu:latest

# base update
RUN apt-get update && apt-get upgrade -y

# add-apt-repository コマンド追加
RUN apt-get install -y apt-file
RUN apt-file update
RUN apt-file search add-apt-repository
RUN apt-get install -y software-properties-common

# gradle & java リポジトリ追加
RUN add-apt-repository ppa:cwchien/gradle
RUN add-apt-repository ppa:rpardini/adoptopenjdk

# gradle & git & maven & ant インストール
RUN apt-get update && apt-get upgrade -y gradle git maven ant

# AdoptOpenJDK 11 インストール
RUN apt-get install -y adoptopenjdk-11-installer
