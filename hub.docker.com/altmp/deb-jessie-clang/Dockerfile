FROM debian:jessie-slim

# production
RUN echo "\n\
deb http://ftp.debian.org/debian jessie main\n\
\ndeb http://ftp.us.debian.org/debian testing main contrib non-free" >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y curl clang-9 libc++-9-dev libc++abi-9-dev lld-9 lldb-9 cmake nodejs
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get install -y yarn
RUN apt-get install -y libc++1
RUN update-alternatives --install /usr/bin/clang clang /usr/bin/clang-9 100 --slave /usr/bin/clang++ clang++ /usr/bin/clang++-9
