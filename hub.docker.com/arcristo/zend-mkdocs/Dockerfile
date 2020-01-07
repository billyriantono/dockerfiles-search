FROM python

MAINTAINER Adiel Cristo <adielcristo@gmail.com>

# Install mkdocs
RUN pip install mkdocs && \
    pip install pymdown-extensions

# Install node
RUN curl -sS https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install yarn

# Install gulp
RUN yarn global add gulp-cli && \
    yarn global add gulp -D

# Install php
RUN apt-get install apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list && \
    apt-get update && \
    apt-get install -y php7.1 php7.1-cli

RUN mkdir -p /workspace

WORKDIR /workspace

ENTRYPOINT ["mkdocs"]

CMD ["serve", "--dev-addr=0.0.0.0:80"]
