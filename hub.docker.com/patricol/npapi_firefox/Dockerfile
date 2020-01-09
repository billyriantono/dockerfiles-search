FROM patricol/gui_base:arch

# firefox-52.9.0esr.tar.bz2 is saved as a binary in this repo for future-proofness; this container is meant for historical preservation of old NPAPI applications.

RUN update \
 && git clone https://aur.archlinux.org/firefox-esr-bin.git \
 && cd ./firefox-esr-bin \
 && git checkout 607696dd7947b6a647aca286a54bb845eef7959e \
 && env FIREFOX_ESR_BIN_PREFER_OLDER=YES makepkg -sci --holdver --noconfirm \
 && cd .. \
 && rm -rf ./firefox-esr-bin \
 && clearcache \
 && echo "exec firefox-esr" >> /scripts/startapp

# For mounting a folder with swf/dcr files etc.
VOLUME /data

# Next steps:
# Disable auto-updating etc.
# Sane basic settings for firefox, so it won't do basic setup every time it is run.
# Include binaries of all necessary NPAPI plugins etc.

# Shockwave never had a linux version. That might actually simplify things; not having to worry about dependencies. Install the windows exes in wine.
