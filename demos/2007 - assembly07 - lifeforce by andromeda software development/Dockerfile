FROM i386/ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y \
    gstreamer1.0-plugins-bad \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-ugly \
    pulseaudio \
    pulseaudio-utils \
    python3-cairo \
    python3-gst-1.0 \
    python3-netifaces \
    python3-pip \
    unzip \
    xterm \
    wine32 \
    xpra

# RUN mkdir /etc/X11/xorg.conf.d && cp /etc/xpra/xorg.conf /etc/X11/xorg.conf.d/00_xpra.conf && \
RUN cp /etc/xpra/xorg.conf /etc/X11/xorg.conf
RUN useradd user && \
    mkdir -p /run/user/1000 /run/xpra && \
    chown user /run/user/1000 /run/xpra && \
    echo "xvfb=Xorg -dpi 96 -noreset -nolisten tcp +extension GLX +extension RANDR +extension RENDER" >> /etc/xpra/xpra.conf

## Install required python modules
RUN pip3 install lz4  pyinotify websockify

## Avoid wine's Mono and Gecko prompts
ENV WINEDLLOVERRIDES "mscoree,mshtml="

##############################################################################

USER user

## Retrieve and extract demoscene files
WORKDIR /home/user/demo/
ADD https://files.scene.org/get/parties/2007/assembly07/demo/lifeforce_by_andromeda_software_development.zip .
RUN unzip *

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
    --start-child=xterm \
    --exit-with-children
