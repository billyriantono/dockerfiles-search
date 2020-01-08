FROM peron/ubuntu-firefox

MAINTAINER peron <per.junel@gmail.com>

USER root

RUN apt-get update && \
    apt-get install -y \
      ca-certificates \
      curl \
      diffuse \
      git \
      --no-install-recommends \
      && rm -rf /var/lib/apt/lists/*

WORKDIR /home/developer/version-control/reflections

RUN curl -sL https://storage.googleapis.com/supplemental_media/udacityu/2997518619/lesson_1_reflection_prompts.txt \
      >> lesson_1_reflection_prompts.txt

USER developer

WORKDIR /home/developer/version-control

VOLUME /home/developer

ENTRYPOINT ["/bin/bash"]
