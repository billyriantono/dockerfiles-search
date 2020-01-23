FROM python

RUN update-ca-certificates -f \
 && curl -sL https://deb.nodesource.com/setup_4.x | bash - \
 && apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y postgresql-client nodejs \
 && apt-get install -y build-essential chrpath libssl-dev libxft-dev \
 && apt-get install -y libfreetype6 libfreetype6-dev \
 && apt-get install -y libfontconfig1 libfontconfig1-dev \
 && apt-get autoremove -y \
 && rm -rf /var/lib/apt/lists/*

ENV PHANTOM_JS phantomjs-1.9.8-linux-x86_64

RUN cd /tmp/ \
 && wget https://bitbucket.org/ariya/phantomjs/downloads/$PHANTOM_JS.tar.bz2 \
 && tar xvjf $PHANTOM_JS.tar.bz2 \
 && rm $PHANTOM_JS.tar.bz2 \
 && mv $PHANTOM_JS /usr/local/share \
 && ln -sf /usr/local/share/$PHANTOM_JS/bin/phantomjs /usr/local/bin

RUN pip install --upgrade pip \
 && pip install setuptools

