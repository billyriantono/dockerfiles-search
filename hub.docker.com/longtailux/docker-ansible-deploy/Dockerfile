# use edge until composer is in latest
From alpine:edge

# install ansible, composer, git, openssh-client and tar
RUN apk add --no-cache ansible composer git openssh-client tar

# install ansistrano
RUN ansible-galaxy install carlosbuenosvinos.ansistrano-deploy
