FROM ubuntu:bionic


RUN useradd -ms /bin/bash liferay
COPY ./script.sh /usr/local/bin/script.sh

RUN chmod +x /usr/local/bin/script.sh
RUN whoami
RUN addgroup liferay root
USER liferay
RUN whoami
ENTRYPOINT ["script.sh"]
