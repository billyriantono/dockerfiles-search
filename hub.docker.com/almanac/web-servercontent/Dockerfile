FROM allmaennitta/dbase:latest
LABEL maintainer.name="Ingo Beyerlein, allmännITta"
LABEL maintainer.mail="ingo.beyerlein@allmaennitta.de"

########## PATHS ##########
ENV PATH=$PATH:/opt/node/bin


########## VERSIONS ##########
#ENV NODEJS_VERSION=8.1.2
ENV NODEJS_VERSION=6.10.0


########## SET UP ##########
WORKDIR "/opt/node"
RUN curl -sL https://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.gz | tar xz --strip-components=1

########## MAIN ##########
RUN npm install -g gulp gulp-cli

########## CLEAN UP ##########
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoremove -y && \
    apt-get clean

CMD bash