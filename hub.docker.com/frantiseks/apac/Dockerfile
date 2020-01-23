FROM java:openjdk-8-jdk
MAINTAINER spacek@fai.utb.cz

# Install wget
RUN apt-get update && apt-get install -y gcc g++ valgrind python mono-vbnc mono-xsp2 mono-xsp2-base mono-mcs && apt-get clean

RUN useradd -ms /bin/bash sandbox
RUN chown -R sandbox:sandbox /home/sandbox
 
USER sandbox
ENV HOME /home/sandbox
