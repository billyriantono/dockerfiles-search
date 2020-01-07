from khronos666/base-image

run apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF
run echo "deb http://repos.mesosphere.io/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/mesosphere.list
run apt-get --yes update