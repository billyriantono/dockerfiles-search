FROM consol/centos-xfce-vnc

## Install Evince Pdf Reader
USER 0
RUN yum install -y evince \
    && yum clean all

### Remove background image
### Overwrite xfce UI config
COPY ./src/xfce4-desktop.xml $HOME/.config/xfce4/xfconf/xfce-perchannel-xml/
RUN rm -f $HOME/.config/bg_sakuli.png

## Add Korean locale
RUN localedef -f UTF-8 -i ko_KR ko_KR.utf8
RUN yum install -y ibus ibus-hangul \
    && yum clean all

## switch back to default user
USER 100

## configure ibus
RUN printf 'ibus-daemon -d -x -r\n\
export GTK_IM_MODULE=ibus\n\
export XMODIFIERS=@im=ibus\n\
export QT_IM_MODULE=ibus\n\
gsettings set org.freedesktop.ibus.general.hotkey triggers "['"'<control>space'"']"'\
>> $HOME/.profile
