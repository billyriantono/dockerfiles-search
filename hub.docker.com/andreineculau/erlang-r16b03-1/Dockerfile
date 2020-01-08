# -*- mode:dockerfile; docker-image-name: "andreineculau/erlang-r16b03-1" -*-

#               andreineculau/erlang-r16b03-1
# version       0.1

from            andreineculau/ubuntu-12.04
maintainer      Andrei Neculau <andrei.neculau@gmail.com>

run             echo deb http://packages.erlang-solutions.com/debian precise contrib >> /etc/apt/sources.list
run             curl -s http://packages.erlang-solutions.com/debian/erlang_solutions.asc | apt-key add -
run             apt-get -y update
run             apt-get install -y erlang=1:16.b.3-3
