FROM          --platform=$TARGETOS/$TARGETARCH python:3.11-slim

LABEL         author="Michael Parker" maintainer="parker@pterodactyl.io"

RUN           mkdir -p /usr/share/man/man1
RUN           apt update \
              && apt -y upgrade \
              && apt -y install \
                     git \
                     ca-certificates \
                     dnsutils \
                     iproute2 \
                     wget \
                     curl \
                     xz-utils \
                     openjdk-17-jre-headless \
                     zlib1g-dev \
                     libffi-dev \
                     libmagickwand-dev \
                     unzip \
                     libaa1-dev \
                     build-essential \
                     tk-dev \
                     libncurses5-dev \
                     libncursesw5-dev \
                     libreadline6-dev \
                     libdb5.3-dev \
                     libgdbm-dev \
                     libsqlite3-dev \
                     libssl-dev \
                     libbz2-dev \
                     libexpat1-dev \
                     liblzma-dev \
                     ffmpeg \
                     imagemagick

RUN           pip install --upgrade pip
RUN           pip install python-forecastio tweepy unidecode mcstatus bs4 sqlalchemy geocoder valve python-valve py-cpuinfo psutil

RUN           mkdir -p /home/container/.config/Red-DiscordBot/
RUN           ln -s /home/container/.config/Red-DiscordBot/ /usr/local/share/Red-DiscordBot

## Setup user and working directory
RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

# Set the locale
RUN        	sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && \
           	locale-gen
ENV      	LANG=en_US.UTF-8
ENV       	LANGUAGE=en_US:en
ENV        	LC_ALL=en_US.UTF-8

COPY        ./entrypoint.sh /entrypoint.sh
CMD         ["/bin/bash", "/entrypoint.sh"]
