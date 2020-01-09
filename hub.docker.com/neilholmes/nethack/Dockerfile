# Set the base
FROM debian
MAINTAINER Neil Holmes

# Install nethack and set up
RUN apt-get update
RUN apt-get -y install apt-utils
RUN apt-get install -y dialog
RUN apt-get install -y nethack-console
RUN apt-get install -y vim
RUN apt-get clean

CMD ["/usr/lib/games/nethack/nethack-console"]
