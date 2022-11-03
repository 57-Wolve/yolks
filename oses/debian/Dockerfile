FROM        --platform=$TARGETOS/$TARGETARCH debian:buster-slim

LABEL       author="Michael Parker" maintainer="parker@pterodactyl.io"

LABEL       org.opencontainers.image.source="https://github.com/57-Wolve/yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN			apt update -y && apt upgrade -y \
			&& dpkg --add-architecture i386 \
			&& apt install -y gcc g++ libgcc1 libstdc++6 lib32gcc1 libc++-dev gdb libc6 git wget curl jq tar zip unzip openssl build-essential binutils xz-utils liblzo2-2 lib32gcc-s1 cabextract iproute2 dirmngr net-tools socat netcat telnet libatomic1 libsdl1.2debian libsdl2-2.0-0 libfontconfig fontconfig libicu63 icu-devtools libunwind8 libssl-dev sqlite3 libsqlite3-dev libmariadbclient-dev libduktape203 locales ffmpeg gnupg2 apt-transport-https software-properties-common ca-certificates tzdata liblua5.3 libz-dev rapidjson-dev libcurl4-gnutls-dev:i386 libssl1.1:i386 libcurl4:i386 lib32tinfo6 libtinfo6:i386 lib32z1 lib32stdc++6 libncurses5:i386 libcurl3-gnutls:i386 libsdl2-2.0-0:i386 gdb libsdl1.2debian libfontconfig1 \
			&& update-locale lang=en_US.UTF-8 \
			&& dpkg-reconfigure --frontend noninteractive locales \
			&& useradd -m -d /home/container -s /bin/bash container
		
RUN			apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
			&& sh -c 'echo "deb https://download.mono-project.com/repo/debian stable-buster main" > /etc/apt/sources.list.d/mono-official-stable.list' \
			&& apt -y update \
			&& apt -y install mono-complete

USER        container
ENV         USER=container HOME=/home/container
ENV         DEBIAN_FRONTEND noninteractive

WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
