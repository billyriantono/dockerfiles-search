FROM ubuntu
RUN apt-get -y update
RUN apt-get install git -y
RUN apt-get install bc git-core gnupg flex bison gperf libsdl1.2-dev squashfs-tools build-essential zip curl libncurses5-dev zlib1g-dev openjdk-8-jre openjdk-8-jdk pngcrush schedtool libxml2 libxml2-utils xsltproc lzop libc6-dev schedtool g++-multilib lib32z1-dev lib32ncurses5-dev gcc-multilib maven tmux screen w3m ncftp -y
RUN mkdir ~/bin
RUN PATH=~/bin:$PATH
RUN curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
RUN chmod a+x ~/bin/repo
RUN mkdir ~/RR && cd ~/RR
RUN apt get install repo -y
RUN repo init -u https://github.com/ResurrectionRemix/platform_manifest.git -b oreo
RUN repo sync -f --force-sync --no-clone-bundle

