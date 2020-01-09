FROM jakubsacha/symfony-docker:php7.2-dev

RUN apt-get update

RUN apt-get install -y zlib1g-dev gnupg apt-transport-https mysql-server

RUN docker-php-ext-install bcmath mysqli zip

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install gd

RUN apt-get install unzip

RUN apt-get --assume-yes install rubygems ruby ruby-dev

RUN gem install sass -v 3.4.5

RUN gem update --system

RUN gem install compass

RUN apt-get --assume-yes install wkhtmltopdf

RUN ln -s /usr/bin/wkhtmltopdf /usr/local/bin/wkhtmltopdf

RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get install -y nodejs yarn

