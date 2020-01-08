FROM python:3.7.0-alpine3.8

WORKDIR /app

# Install bash
RUN apk add --no-cache bash gawk sed grep bc coreutils

# Install cloc
RUN apk add cloc

# Install curl
RUN apk add --no-cache curl

# Install utils like column
RUN apk add util-linux

# Install jq
RUN apk --update add jq && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

# Install git
RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

# Create directories
RUN mkdir /report

# Install Git Extras
RUN git clone https://github.com/tj/git-extras.git /tmp/git-extras
#RUN cp /tmp/git-extras/bin/git-effort /usr/bin
RUN cp /tmp/git-extras/bin/git-count /usr/bin
RUN cp /tmp/git-extras/bin/git-changelog /usr/bin
RUN cp /tmp/git-extras/bin/git-summary /usr/bin
RUN cp /tmp/git-extras/bin/git-count /usr/bin
RUN cp /tmp/git-extras/bin/git-root /usr/bin

COPY ./git_effort.sh /usr/bin/git_effort
RUN chmod +x /usr/bin/git_effort

COPY ./git_changelog.sh /usr/bin/git_changelog
RUN chmod +x /usr/bin/git_changelog

ADD entrypoint.sh /
ADD get-cloc /usr/bin/get-cloc
ADD get-changelog /usr/bin/get-changelog
ADD get-count /usr/bin/get-count
ADD get-count-commits-per-day /usr/bin/get-count-commits-per-day
ADD get-count-updated-lines-per-day /usr/bin/get-count-updated-lines-per-day
ADD get-effort /usr/bin/get-effort
ADD get-list-branch-not-merged /usr/bin/get-list-branch-not-merged
ADD get-list-branch-per-date /usr/bin/get-list-branch-per-date
ADD get-log /usr/bin/get-log
ADD get-repo-size /usr/bin/get-repo-size
ADD get-stats /usr/bin/get-stats
ADD get-summary /usr/bin/get-summary

# Copy scripts
COPY csv2json.jq /app/
COPY requirements.txt /app/
RUN pip install --trusted-host pypi.python.org -r requirements.txt
EXPOSE 5200
WORKDIR /src

ENTRYPOINT ["/entrypoint.sh"]
