FROM debian:9.8-slim

LABEL author.name="Anderson F"                    \
      author.email="andersonsergipano@gmail.com"  \
      build.date="2019-03-28"                      \
      version="0.1"                                            \
      description.summary="Image that provides java openjdk 11" \
      description.details.1="Why am I using Debian a instead of Alpine?  Because Oracle OpenJDK uses GLiC and Alpine uses musl." \
      java.implementation.vendor="Oracle OpenJDK" \
      java.implementation.version="11.0.2"

ARG java_tar_url="https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz"
ARG java_folder="/opt/java"
ARG slinks_folder="/usr/bin"

RUN echo "                                                        " && \
echo "   JAVA INSTALLATION SCRIPT                                 " && \
echo "   by ANDERSON                                              " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Configuring Variables                                      " && \
echo "------------------------------------------------------------" && \
   PKGS="wget"                                                      && \
   TAR_NAME="java.tar.gz"                                           && \
echo "                                                            " && \
echo " Configuration completed                                    " && \
echo "                                                            " && \
echo " Starting the work. Lets go...                              " && \
echo "                                                            " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Installing Required Packages                               " && \
echo "------------------------------------------------------------" && \
echo "                                                            " && \
   apt -y update < /dev/null                                        && \
   apt -y install $PKGS < /dev/null                                 && \
echo "                                                            " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Downloading OpenJDK                                        " && \
echo "------------------------------------------------------------" && \
echo "                                                            " && \
   wget -v -c $java_tar_url -O ./$TAR_NAME                          && \
echo "                                                            " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Decompressing tar file                                     " && \
echo "------------------------------------------------------------" && \
echo "                                                            " && \
   OLD_FOLDER=$(tar -tzf ./$TAR_NAME | head -1 | cut -f1 -d "/")    && \
   tar -xvzf ./$TAR_NAME                                            && \
   mv ./$OLD_FOLDER $java_folder                                    && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Fixing folder permissions                                  " && \
echo "------------------------------------------------------------" && \
echo "                                                            " && \
   chmod -v -R 755 $java_folder                                     && \
echo "                                                            " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Creating Symbolics links                                   " && \
echo "------------------------------------------------------------" && \
echo "                                                            " && \
echo " Adding All Java's binaries                                 " && \
   for filename in $(ls $java_folder/bin);                             \
      do ln -v -s $java_folder/bin/$filename $slinks_folder/$filename; \
   done                                                             && \
echo "                                                            " && \
echo " Adding the exception: jexec                                " && \
   ln -v -s $java_folder/lib/jexec $slinks_folder/jexec             && \
echo "                                                            " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " INITIALIZING CLEANING...                                   " && \
echo "------------------------------------------------------------" && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Deleting Java tar.gz file                                  " && \
echo "------------------------------------------------------------" && \
   rm -f -v $TAR_NAME                                               && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Removing packages binaries and configuration files         " && \
echo "------------------------------------------------------------" && \
   apt -y purge --auto-remove $PKGS < /dev/null                     && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Cleaning cache                                             " && \
echo "------------------------------------------------------------" && \
   apt -y clean < /dev/null                                         && \
   rm -rfv /var/cache/apt/*                                         && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Undoing apt update                                         " && \
echo "------------------------------------------------------------" && \
   rm -rfv /var/lib/apt/lists/*                                     && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Cleaning folders logs                                      " && \
echo "------------------------------------------------------------" && \
   rm -dfv /var/log/apt/*                                           && \
   rm -dfv /var/log/*                                               && \
echo "                                                            " && \
echo "                                                            " && \
echo "------------------------------------------------------------" && \
echo " Script finished - Thank you for your attention             " && \
echo "------------------------------------------------------------"

ENV JAVA_HOME="$java_folder"
ENV JDK_HOME="$java_folder"
ENV CLASSPATH="$java_folder/lib"

CMD ["/bin/bash"]
