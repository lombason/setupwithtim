FROM ubuntu:latest
ADD https://dl.winehq.org/wine-builds/winehq.key /winehq.key


ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
	apt-get install -y gnupg apt-utils && \
	echo "deb http://dl.winehq.org/wine-builds/ubuntu/ focal main" >> /etc/apt/sources.list && \
	apt-key add /winehq.key && \
	mv /winehq.key /usr/share/keyrings/winehq-archive.key && \
	dpkg --add-architecture i386 && \
	apt-get update && \
	apt-get install -y -q --install-recommends winehq-devel && \
	rm -rf /var/lib/apt/lists/* /winehq.key
RUN groupadd -g 1000 wine \
	&& useradd -g wine -u 1000 wine \
	&& mkdir -p /home/wine/.wine && chown -R wine:wine /home/wine
USER wine
ENTRYPOINT [ "wine" ]
CMD [ "/MetaTrader/terminal64.exe", "/portable" ]
