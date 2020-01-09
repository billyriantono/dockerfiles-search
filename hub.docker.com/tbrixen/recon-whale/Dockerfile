from ubuntu:19.10 as masscan

RUN apt-get update && apt-get install -y \
    gcc \
    git\
    libpcap-dev\
    make
RUN git clone https://github.com/robertdavidgraham/masscan /masscan \
    && cd /masscan \
    && make

FROM ubuntu:19.10 as amass-and-subfinder
RUN apt-get update && apt-get install -y \
    gcc \
    git

ADD https://dl.google.com/go/go1.13.linux-amd64.tar.gz /tmp/go.tar.gz
RUN tar -C /usr/local -xzf /tmp/go.tar.gz
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

RUN go get github.com/OWASP/Amass; exit 0
ENV GO111MODULE on
WORKDIR /go/src/github.com/OWASP/Amass
RUN go install ./...

RUN go get github.com/subfinder/subfinder; exit 0
ENV GO111MODULE on
WORKDIR /go/src/github.com/subfinder/subfinder
RUN go install ./...

FROM ubuntu:19.10 as massdns

RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    libldns-dev \
    python
RUN git clone https://github.com/blechschmidt/massdns.git /massdns \
    && cd /massdns \
    && make

FROM ubuntu:19.10

RUN apt-get update && apt-get install -y \
    git \
    curl \
    jq \
    nmap \
    python3 \
    python3-pip \
    vim \
    && pip3 install --upgrade pip

RUN mkdir -p /lists/jhaddix && \
    curl https://gist.githubusercontent.com/jhaddix/86a06c5dc309d08580a018c66354a056/raw/96f4e51d96b2203f19f6381c8c545b278eaa0837/all.txt -o /lists/jhaddix/subdomains.txt

RUN mkdir /tools/
RUN git clone https://github.com/FortyNorthSecurity/EyeWitness.git /tools/EyeWitness && \
  /tools/EyeWitness/setup/setup.sh
ENV PATH /tools/EyeWitness:$PATH

RUN git clone https://github.com/maurosoria/dirsearch.git /tools/dirsearch
ENV PATH /tools/dirsearch:$PATH

RUN git clone https://github.com/christophetd/censys-subdomain-finder.git /tools/censys-subdomain-finder && \
    pip3 install -r /tools/censys-subdomain-finder/requirements.txt && \
    chmod u+x /tools/censys-subdomain-finder/censys_subdomain_finder.py
ENV PATH /tools/censys-subdomain-finder:$PATH

RUN git clone https://github.com/lanmaster53/recon-ng.git /tools/recon-ng && \
    pip3 install -r /tools/recon-ng/REQUIREMENTS
ENV PATH /tools/recon-ng:$PATH

RUN curl -sL https://github.com/tomnomnom/gron/releases/download/v0.6.0/gron-linux-amd64-0.6.0.tgz | tar -zxC /usr/bin/

RUN curl -sL https://github.com/tomnomnom/httprobe/releases/download/v0.1.2/httprobe-linux-amd64-0.1.2.tgz | tar -zxC /usr/bin/

COPY --from=amass-and-subfinder /go/bin/amass /usr/bin/amass
COPY --from=masscan /masscan/bin/masscan /usr/bin/masscan
COPY --from=massdns /massdns/bin/massdns/ /usr/bin/massdns
COPY --from=massdns /massdns/lists/resolvers.txt/ /lists/massdns/resolvers.txt
COPY --from=amass-and-subfinder /go/bin/subfinder /usr/bin/subfinder

