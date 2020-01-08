FROM ubuntu:latest
ENV TERM=xterm
RUN apt-get -qq update && \
    apt-get -qq install -y git \
                curl \
                ca-certificates \
                libgtk2.0-0 \
                libxtst6 \
                libnss3 \
                libgconf-2-4 \
                libasound2 \
                fakeroot \
                gconf2 \
                gconf-service \
                libcap2 \
                libnotify4 \
                libxtst6 \
                libnss3 \
                gvfs-bin \
                xdg-utils \
                composer \
		libxss1 \
		libxkbfile1 \
                python && \
    apt-get clean && \
    curl -L https://atom.io/download/deb > /tmp/atom.deb && \
    dpkg -i /tmp/atom.deb && \
    rm -f /tmp/atom.deb
    
VOLUME /workspace

CMD ["/usr/bin/atom","-f", "/workspace"]
