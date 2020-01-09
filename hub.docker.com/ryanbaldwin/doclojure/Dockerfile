# Creates a new image with user clj:clj. 
# Also installs leiningen (most recent version).
FROM ryanbaldwin/oracle-jdk:7
MAINTAINER Ryan Baldwin <ryanbaldwin@gmail.com>

# create the clj user
RUN addgroup clj && \
    adduser --disabled-password --disabled-login --ingroup clj clj

# install leiningen
RUN cd /bin && \
    wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein && \
    chmod a+x /bin/lein && \
    setuser clj lein

# install git, because clojure without git is like a hug without a squeeze
RUN apt-get -y -qq --force-yes  update && \
    apt-get -y -qq --force-yes  install git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*