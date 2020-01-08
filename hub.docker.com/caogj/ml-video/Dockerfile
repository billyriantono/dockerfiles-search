FROM ubuntu

RUN apt update && apt install -y curl python
RUN curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/bin/youtube-dl && chmod a+rx /usr/bin/youtube-dl
RUN youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best' -o '%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s' 'https://www.youtube.com/watch?v=Tk5B4seA-AU'
