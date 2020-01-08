FROM docker.elastic.co/kibana/kibana-oss:6.0.0

ENV KIBANA_VER_MAJOR="6"
ENV KIBANA_VER_MINOR="0"
ENV KIBANA_VER_PATCH="0"

ENV KIBANA_VER_MAJOR_MINOR="$KIBANA_VER_MAJOR.$KIBANA_VER_MINOR"
ENV KIBANA_VER_MAJOR_MINOR_PATCH="$KIBANA_VER_MAJOR.$KIBANA_VER_MINOR.$KIBANA_VER_PATCH"

LABEL maintainer "Angry Cactus DevOps Team <devops@angrycactus.io>"
LABEL version="$KIBANA_VER_MAJOR_MINOR_PATCH"
LABEL description="Kibana Docker image with the x-pack plugin removed and couple visualization plugins installed."

# Override the kibana-docker binary.
# https://github.com/elastic/kibana-docker/blob/5.6/templates/Dockerfile.j2#L29
ADD ./build/bin/kibana-docker /usr/local/bin/

# Remove X-PACK plugin.
# RUN kibana-plugin remove x-pack

# Install Own Home plugin.
RUN kibana-plugin install https://github.com/wtakase/kibana-own-home/releases/download/v$KIBANA_VER_MAJOR_MINOR_PATCH/own_home-$KIBANA_VER_MAJOR_MINOR_PATCH.zip

CMD ["/bin/bash", "/usr/local/bin/kibana-docker"]
