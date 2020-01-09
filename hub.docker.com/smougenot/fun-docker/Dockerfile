#
# Some fun (based on an original idea from @dgageot)
#
# -> default use cowsay
#  - try -l to list templates
# -> then you can try /usr/games/sl
# -> if you dare, try the matrix /usr/bin/cmatrix
# -> or watch the first Star Wars over telnet @ towel.blinkenlights.nl
#
FROM ubuntu:trusty
MAINTAINER sylvain.mougenot@gmail.com

# download and install java
RUN apt-get update 
RUN apt-get install -y --no-install-recommends \
	  fortune cowsay sl telnet
RUN apt-get install -y --no-install-recommends \
	  cmatrix

ENTRYPOINT ["/usr/games/cowsay"]
CMD ["hello"]
