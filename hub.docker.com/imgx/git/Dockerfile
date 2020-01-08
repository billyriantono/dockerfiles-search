FROM alpine
LABEL maintainer Chanson X <cs.x@icloud.com>
RUN apk --no-cache add zsh git openssh
RUN sed -i -e "s/bin\/ash/bin\/zsh/" /etc/passwd
ENV SHELL /bin/zsh
VOLUME /root
ENTRYPOINT ["zsh"]
# CMD ["zsh"]
