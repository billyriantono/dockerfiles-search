FROM kylef/swiftenv:swift3
MAINTAINER Valentin Knabel <dev@vknabel.com>

ENV ROCK_PATH "/home/.rock"
ENV PATH "./.rock/bin:$ROCK_PATH/bin:$PATH"

RUN curl -sL https://raw.githubusercontent.com/vknabel/Rock/master/Scripts/Install.generated.swift | swift -
