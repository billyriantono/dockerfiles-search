FROM golang:latest

# Install node and Python
RUN apt-get purge -y python.*
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -
RUN apt-get update && apt-get install -y --no-install-recommends nodejs python python-pip zip && rm -rf /var/lib/apt/lists/*

# Install Electron tools
RUN npm install electron-packager -g
RUN npm install electron-builder -g

# Install GOX
RUN go get github.com/mitchellh/gox
RUN go get github.com/aktau/github-release

# Install AWS CLI
RUN pip install awscli

CMD ["bash"]