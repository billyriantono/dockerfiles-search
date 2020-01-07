FROM  codercom/code-server:latest
RUN cd ~\
  && sudo su \
  && sudo apt-get update \
  && sudo apt-get install openjdk-11-jre-headless -y

# Install Leiningen
RUN sudo su \
#  && sudo apt-get install leiningen -y
   && sudo curl -O https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein \
   && sudo cp ./lein /usr/local/bin/lein \
   && sudo chmod +x /usr/local/bin/lein \
   && sudo lein

# Install shadow-cljs
RUN sudo su \
 && sudo apt-get install nodejs npm rlwrap -y \
 && sudo npm install -g shadow-cljs yarn

#install clojure
RUN  sudo curl -O https://download.clojure.org/install/linux-install-1.10.0.442.sh \
    && sudo chmod +x linux-install-1.10.0.442.sh \ 
    && sudo ./linux-install-1.10.0.442.sh \
    && clojure -e 1

 #install vs coder extension
 RUN sudo apt-get install bsdtar -y \
    && curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/cospaia/vsextensions/clojure4vscode/1.3.65/vspackage | bsdtar -xvf - extension \
    && mkdir -p /home/coder/.local/share/code-server/extensions \
    && mv extension /home/coder/.local/share/code-server/extensions/clojure4vscode-1.3.65 \
    && curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/shaunlebron/vsextensions/vscode-parinfer/0.6.2/vspackage | bsdtar -xvf - extension \
    && mv extension /home/coder/.local/share/code-server/extensions/parinfer-0.6.2 \
    && curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/CoenraadS/vsextensions/bracket-pair-colorizer-2/0.0.28/vspackage | bsdtar -xvf - extension \
    && mv extension /home/coder/.local/share/code-server/extensions/bracket-pair-colorizer-2-0.0.28 

# try to clean up
RUN sudo rm -rf /tmp/* \
 && sudo rm -rf /var/lib/apt/lists/*

EXPOSE 8443

CMD [ "code-server" ]
ENTRYPOINT [ "code-server"]