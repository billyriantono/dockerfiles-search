FROM ubuntu:19.04
RUN apt-get update && apt-get install -y perl build-essential cpanminus
RUN [ "cpanm", "Test::Script::Run", "Test::More" ]
