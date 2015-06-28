# Run skype in a container, requires pulseaudio
# (container desktop-docker-pulseaudio linked for this)
#
# docker run -v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	--link pulseaudio:pulseaudio \
#	-e PULSE_SERVER=pulseaudio \
#	--device /dev/video0 \
#	cloudconsulted/desktop-docker-skype
#
FROM debian:jessie
MAINTAINER John Wooten/CONSULTED <jwooten@cloudconsulted.com>

# Tell debconf to run in non-interactive mode
ENV DEBIAN_FRONTEND noninteractive

# Setup multiarch because Skype is 32bit only
# Make sure the repository information is up to date
RUN dpkg --add-architecture i386 && \
	apt-get update && apt-get install -y \
	curl \
	--no-install-recommends


# Install Skype
RUN curl http://download.skype.com/linux/skype-debian_4.3.0.37-1_i386.deb > /usr/src/skype.deb && \ 
	dpkg -i /usr/src/skype.deb && \
	apt-get install -fy \
	&& rm -rf /var/lib/apt/lists/*

# Start Skype
ENTRYPOINT ["skype"]
