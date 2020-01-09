FROM thies88/base-alpine

MAINTAINER thies88

ENV gituser="example"
ENV gitfolder="/opt/git"
ENV gitrepo="example"
ENV giturl="https://github.com/example/example"

# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │
# │ │ │ │ │
# * * * * * command to execute
ENV croninterval="0 3 * * 6"

RUN apk update
RUN apk add --no-cache git openssh openssh-keygen

#copy local files
COPY /root /
