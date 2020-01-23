#########################################################################
# Copyright (C) 2018-2019 Andres Castellanos                            #
#                                                                       #
# This program is free software: you can redistribute it and/or modify  #
# it under the terms of the GNU General Public License as published by  #
# the Free Software Foundation, either version 3 of the License, or     #
# (at your option) any later version.                                   #
#                                                                       #
# This program is distributed in the hope that it will be useful,       #
# but WITHOUT ANY WARRANTY; without even the implied warranty of        #
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         #
# GNU General Public License for more details.                          #
#                                                                       #
# You should have received a copy of the GNU General Public License     #
# along with this program.  If not, see <https://www.gnu.org/licenses/> #
#########################################################################

FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install --no-install-recommends wget unzip -y && \
    wget --no-check-certificate https://github.com/andrescv/Jupiter/releases/download/v3.1/Jupiter-3.1-linux.zip && \
    unzip Jupiter-3.1-linux.zip && mv image /opt/jupiter && rm -f Jupiter-3.1-linux.zip && \
    echo '#!/bin/sh' > /usr/bin/jupiter && \
    echo '/opt/jupiter/bin/java --add-exports javafx.controls/com.sun.javafx.scene.control=com.jfoenix --add-exports javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix --add-exports javafx.graphics/com.sun.javafx.scene=com.jfoenix -m jupiter/jupiter.Jupiter  "$@"' >> /usr/bin/jupiter && \
    chmod +x /usr/bin/jupiter && \
    apt-get purge wget unzip -y && \
    apt-get clean -y && apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/bin/jupiter"]

CMD ["-h"]
