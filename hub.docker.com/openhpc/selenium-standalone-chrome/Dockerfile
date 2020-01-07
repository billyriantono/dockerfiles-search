FROM selenium/standalone-chrome-debug

LABEL name="Selenium Standalone Chrome Debug" \
    maintainer="gaojingan@gmail.com"

RUN sudo apt-get -y update \
  && sudo apt-get -y install ttf-wqy-microhei ttf-wqy-zenhei curl \
  && sudo apt-get -y clean \
  && curl https://bootstrap.pypa.io/get-pip.py| sudo python3 \
  && sudo ln -svf /usr/bin/python3 /usr/bin/python \
  && sudo pip install selenium behave nose pillow ipython

EXPOSE 4444
EXPOSE 5900

CMD ["/opt/bin/entry_point.sh"]
