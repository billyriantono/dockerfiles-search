FROM node:lts

RUN apt update
RUN wget https://go.microsoft.com/fwlink/?LinkID=760868 -O vscode.deb

#Install VSCode always fails because of missing dependencies, the next command will do the trick
RUN dpkg -i vscode.deb || true
RUN apt-get install -y -f && apt clean all && rm -f vscode.deb

#Some functions of NPM would not be allowed to run as root, that's why we need a builder account 
#RUN useradd -ms /bin/bash builder

#The trick from https://medium.com/@bhadrajatin/docker-volume-mount-as-non-root-77ffae5a79d0
#RUN mkdir /src && chown -R builder:builder /src
#USER builder

WORKDIR /src

CMD ["node"]
