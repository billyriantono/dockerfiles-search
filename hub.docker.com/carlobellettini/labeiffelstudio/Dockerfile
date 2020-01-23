FROM carlobellettini/eiffelstudio
MAINTAINER Carlo Bellettini

USER root
RUN apt-get -y install git
RUN apt-get -y install gitg
RUN apt-get -y install rxvt 
RUN apt-get -y install vim


USER eiffel

RUN git config --global alias.hist  "log --pretty=format:'%Cred%h%Creset %C(bold blue)<%an>%Creset%C(yellow)%d%Creset %Cgreen(%cr)%Creset%n%w(80,8,8)%s' --graph"

RUN mkdir -p /home/eiffel/.es/eiffel_user_files/15.08 && \
    echo "">> /home/eiffel/.es/eiffel_user_files/15.08/external_commands.ini && \
    echo "/home/eiffel/.es/eiffel_user_files/15.08">> /home/eiffel/.es/eiffel_user_files/15.08/external_commands.ini && \
    echo "0 = xterm{0{rxvt -e bash{/home/eiffel">> /home/eiffel/.es/eiffel_user_files/15.08/external_commands.ini && \
    echo "1 = gitg{1{gitg{/home/eiffel/repo">> /home/eiffel/.es/eiffel_user_files/15.08/external_commands.ini
