FROM unidata/thredds-docker

MAINTAINER HDizzle

#so the repository lists can be update
RUN apt-get update -y

#needed for ssh
EXPOSE 22

# run ssh start in detached mode
CMD ["/etc/init.d/ssh", "start", "-D"]
