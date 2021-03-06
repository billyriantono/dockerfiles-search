# alpine linux novnc

FROM youske/alpine-stdmachine:base
MAINTAINER youske miyakoshi <youske@gmail.com>

# Set correct environment variables.
ENV HOME=/root
ENV PORT=8080
ENV DISPLAYSIZE=${XDISPLAY_WIDTH}"x"${XDISPLAY_WIDTH}"x"${XDISPLAY_DEPTH}
ENV DEBIAN_FRONTEND=noninteractive

ENV LC_ALL=C.UTF-8
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=${LANG}
ENV TZ=Asia/Tokyo

RUN apk --update add tzdata --no-cache && \
    cp /usr/share/zoneinfo/${TZ} /etc/localtime && echo $TZ > /etc/timezone && \
    apk del tzdata && \
    # Installing apps and clean up.
    PACKAGE="wget ca-certificates git bash python xvfb x11vnc ttf-noto fluxbox net-tools socat supervisor xterm " && \
    apk update upgrade --no-cache && apk add --no-cache ${PACKAGE} && \
    # noVNC download
    git clone https://github.com/kanaka/noVNC.git /opt/noVNC && \
    git clone https://github.com/kanaka/websockify /opt/websockify && \
    ln -sf /opt/websockify /opt/noVNC/utils/websockify && \
    ln -s /opt/noVNC/vnc.html /opt/noVNC/index.html && \
    rm -rf /opt/noVNC/.git && \
    rm -rf /opt/websockify/.git

# chromium browser
#RUN apt-get install -y chromium-browser
#RUN sed -i -- "s/ps -p/ps -o pid | grep/g" /opt/noVNC/utils/launch.sh

# Configure & run supervisor
EXPOSE ${PORT} 6000
COPY novnc.conf /etc/supervisor/conf.d/novnc.conf
ENTRYPOINT ["switch","shell=/bin/bash","--","/init"]
#ENTRYPOINT ["render","/etc/supervisor/conf.d/novnc.conf","--","switch","shell=/bin/bash","--","/init"]
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/novnc.conf"]
