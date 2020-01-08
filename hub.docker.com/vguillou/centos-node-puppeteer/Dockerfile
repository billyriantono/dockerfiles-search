FROM vguillou/centos-node:7.7-10.16.3

RUN yum -y install epel-release \
 && yum -y install pango.x86_64 pango-devel.x86_64 libXcomposite.x86_64 libXcursor.x86_64 libXdamage.x86_64 \
 libXext.x86_64 libXi.x86_64 libXtst.x86_64 cups-libs.x86_64 libXScrnSaver.x86_64 \
 libXrandr.x86_64 GConf2.x86_64 alsa-lib.x86_64 atk.x86_64 gtk3.x86_64 \
 pixman.x86_64 pixman-devel.x86_64 cairo.x86_64 cairo-devel.x86_64 libjpeg-turbo.x86_64 libjpeg-turbo-devel.x86_64 \
 ipa-gothic-fonts cabextract xorg-x11-utils xorg-x11-font-utils fontconfig \
 xorg-x11-fonts-100dpi xorg-x11-fonts-75dpi xorg-x11-fonts-cyrillic xorg-x11-fonts-Type1 xorg-x11-fonts-misc \
 open-sans-fonts liberation-fonts \
 && yum -y groupinstall "Font" \
 && rpm -iv https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm \
 && yum clean all \
 && rm -rf /var/cache/yum
