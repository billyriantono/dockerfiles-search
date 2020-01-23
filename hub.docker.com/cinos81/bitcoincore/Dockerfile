FROM ubuntu:16.04
LABEL "STEP"="0"
#sudo를 설치한다
RUN apt-get update && \
    apt-get install -y sudo && \
    rm -rf /var/lib/apt/lists/*
#git을 설치하기 위한 apt 리파지토리를 추가한다
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E1DD270288B4E6030699E45FA1715D88E1DF1F24
RUN sudo su -c "echo 'deb http://ppa.launchpad.net/git-core/ppa/ubuntu trusty main' > /etc/apt/sources.list.d/git.list"
#다시 apt-get을 업데이트
RUN apt-get update

LABEL "STEP"="1"
# Bitcoin Core 의 소스 코드와 라이브러리를 다운로드 받는다
RUN mkdir src && \
    cd src && \
    sudo apt-get install -y git && \
    git clone https://github.com/bitcoin/bitcoin.git
#gcc, OpenSSl을 설치한다
RUN sudo apt-get install -y build-essential automake pkg-config libevent-dev bsdmainutils
RUN sudo apt-get install -y libtool autotools-dev autoconf
RUN sudo apt-get install -y libssl-dev

LABEL "STEP"="2"
#libdb4.8설치 && bitcoin 리파지토리 등록
RUN apt-get install -y software-properties-common && \
    sudo add-apt-repository ppa:bitcoin/bitcoin
#다시 apt-get을 업데이트
RUN apt-get update
#libdb4.8을 설치
RUN apt-get install -y libdb4.8-dev libdb4.8++-dev

LABEL "STEP"="3"
#관련 라이브러리를 설치한다
RUN apt-get install -y libminiupnpc-dev libqrencode-dev libboost-all-dev

LABEL "STEP"="4"
#GUI 라이브러리를 설치한다
RUN apt-get install -y libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

LABEL "STEP"="5"
#Bitcoin Core빌드
RUN cd src/bitcoin && ./autogen.sh && ./configure && make
#설치
RUN cd src/bitcoin && make install && cd src/bitcoin
#비드코인 데몬 실행
CMD bitcoind -regtest
