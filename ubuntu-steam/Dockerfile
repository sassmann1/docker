FROM ubuntu

RUN echo 'deb [arch=amd64,i386] http://repo.steampowered.com/steam precise steam' > /etc/apt/sources.list.d/steam-inst.list && dpkg --add-architecture i386
RUN apt-get update && apt-get install -yq --no-install-recommends --force-yes sudo libgl1-mesa-dri steam pulseaudio
RUN rm -rf /etc/apt/sources.list.d/steam-inst.list
RUN apt-get update && apt-get install -yq libgl1-mesa-dri:i386 libgl1-mesa-glx:i386 libc6:i386 libnss3:i386 dbus:i386

RUN echo 'steam ALL = NOPASSWD: ALL' > /etc/sudoers.d/steam
RUN chmod 0440 /etc/sudoers.d/steam
RUN adduser --disabled-password --gecos 'Steam' steam
RUN ln -s /bin/dbus-daemon /usr/bin/dbus-daemon

USER steam
ENV HOME /home/steam
VOLUME /home/steam
ENV PULSE_SERVER unix:/tmp/pulse
CMD sudo /etc/init.d/dbus start && steam