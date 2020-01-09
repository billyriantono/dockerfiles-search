FROM circleci/node:10.16.3-buster-browsers

# install Allure
RUN ALLURE_VERSION="2.12.1" \
 && ALLURE_ARCHIVE_SHA1="4644f17d64e80230c00c7e8ec811a1fe2294f070" \
 && curl --silent --show-error --location --fail --retry 4 --retry-delay 5 \
         --output /tmp/allure.zip \
         "http://repo.maven.apache.org/maven2/io/qameta/allure/allure-commandline/${ALLURE_VERSION}/allure-commandline-${ALLURE_VERSION}.zip" \
 && cd /tmp \
 && echo "${ALLURE_ARCHIVE_SHA1} *allure.zip" | sha1sum -c --quiet - \
 && sudo unzip -qq allure.zip \
 && rm -rf allure.zip \
 && sudo mv "allure-${ALLURE_VERSION}" /usr/local/share/allure \
 && sudo ln -s /usr/local/share/allure/bin/allure /usr/local/bin/allure \
 && allure --version

# install Japanise fonts
RUN sudo apt-get update -qq \
 && sudo apt-get install -qq -y \
                         fonts-noto-color-emoji \
                         fonts-takao-mincho

# install chores
RUN sudo apt-get install -qq -y \
                         less \
                         vim \
 && echo noswapfile >> $HOME/.vimrc
