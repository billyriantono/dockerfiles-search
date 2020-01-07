FROM golang:1-stretch

# install mingw64 cross compilation tool
RUN apt-get update && apt-get install -y \
	mingw-w64-* \
  && rm -rf /var/lib/apt/lists/*

# install go official dep tool
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

