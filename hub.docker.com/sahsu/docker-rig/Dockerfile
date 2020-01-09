FROM elyase/staticpython

MAINTAINER sahsu.mobi@gmail.com

ADD https://github.com/HoverHell/RedditImageGrab/archive/master.zip /
RUN unzip /master.zip

ENTRYPOINT ["/RedditImageGrab-master/redditdl.py"]
