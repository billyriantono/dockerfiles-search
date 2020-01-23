FROM nginx

RUN apt-get update \
 && apt-get install -y \
      git \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && git clone https://github.com/novnc/noVNC.git \
 && mv noVNC/* /usr/share/nginx/html/
