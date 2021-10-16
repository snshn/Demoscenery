FROM i386/alpine:3.13.5

RUN apk add --update --no-cache \
    cabextract \
    gst-plugins-bad \
    gst-plugins-good \
    gst-plugins-ugly \
    mesa-dri-gallium \
    pulseaudio \
    pulseaudio-utils \
    py3-cairo \
    py3-gst \
    py3-netifaces \
    py3-pip \
    shadow \
    st \
    wine \
    xpra

RUN cp /etc/xpra/xorg.conf /etc/X11/xorg.conf.d/00_xpra.conf && \
    adduser -D user && \
    mkdir -p /run/user/1000 /run/xpra && \
    chown user /run/user/1000 /run/xpra && \
    echo "xvfb=Xorg -dpi 96 -noreset -nolisten tcp +extension GLX +extension RANDR +extension RENDER" >> /etc/xpra/xpra.conf

## Install required python modules
RUN pip3 install lz4 pyinotify websockify

## Workaround for gst-plugin-scanner's bug
RUN ln -s /usr/lib/libpython3.8.so.1.0 /usr/lib/libpython3.8.so

## Avoid wine's Mono and Gecko prompts
ENV WINEDLLOVERRIDES "mscoree,mshtml="

##############################################################################

## X
RUN wget -O /usr/bin/winetricks https://github.com/Winetricks/winetricks/raw/dbcd548f81025a5800f2020c0d4ed2c0b0755477/src/winetricks
RUN chmod +x /usr/bin/winetricks
RUN sed -i "s/--read-timeout 300//g" /usr/bin/winetricks
RUN sed -i "s/--retry-connrefused//g" /usr/bin/winetricks

## Retrieve and extract demoscene files
USER user
WORKDIR /home/user/demo/
ADD https://files.scene.org/get/parties/2000/assembly00/demo/further_.zip .
RUN unzip *

# RUN winetricks mfc42

## Run Xpra
EXPOSE 10000
CMD xpra start \
    --html=on \
    --daemon=no \
    --notifications=no \
    --dbus-proxy=no \
    --no-microphone \
    --speaker \
    --encoding=rgb \
    --no-tray \
    --mdns=no \
    --bind-tcp=0.0.0.0:10000 \
    --start-child=st \
    --exit-with-children
