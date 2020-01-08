FROM guilhermesilveira/java8
MAINTAINER Guilherme Silveira "guilherme.silveira@alura.com.br"
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list
RUN mkdir -p /usr/share/desktop-directories
RUN apt-get -qq update -y

#TODO: fixar firefox=28.0+build2-0ubuntu2
#

RUN apt-get install -y -qq x11vnc xvfb xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic

# version-sensitive stuff later on because they might change often

# selenium as last as its version might update often
RUN npm install -g selenium-standalone@2.42.2-2.9.0-2

# downloading firefox 28
RUN apt-get install -y libasound2 libgtk2.0-0
RUN mkdir -p /home/root
RUN wget -q -O - http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/28.0/linux-x86_64/en-US/firefox-28.0.tar.bz2 | tar jxf - -C /home/root/
RUN ln -s /home/root/firefox/ /usr/local/firefox
RUN ln -s /usr/local/firefox/firefox /usr/bin/firefox

# unsafe chrome version, we don't know which version will be installed
RUN useradd -d /home/chromeuser -m chromeuser
RUN mkdir -p /home/chromeuser/chrome
RUN chown chromeuser /home/chromeuser/chrome
RUN chgrp chromeuser /home/chromeuser/chrome
RUN apt-get install -y -q google-chrome-beta 

ADD ./scripts/ /home/root/scripts
EXPOSE 4444
EXPOSE 5999
ENTRYPOINT ["sh", "/home/root/scripts/start.sh"]