FROM node:4.4.4-wheezy
MAINTAINER "Cristian Martínez" <cristianandres92@gmail.com>

# Install git, sudo
RUN apt-get -yq update && \
    apt-get -yq install git sudo && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Add a angularexample
RUN adduser --disabled-password --gecos '' angularexample && \
	adduser angularexample sudo && \
  	echo "%sudo ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
# Set HOME
ENV HOME /home/angularexample

# Install lib dependencies
RUN apt-get -yq update && \
    apt-get -yq install xdg-utils bzip2 libfreetype6 libfontconfig && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install apps
RUN npm install -g gulp grunt-cli bower python phantomjs \
        jasmine-core karma-cli karma-phantomjs-launcher --save-dev \
        karma-jasmine --save-dev node-pre-gyp && \
    npm install karma --save-dev && \
    rm -rf ~/.npm && npm cache clear

# Install server
RUN npm install http-server -g && \
    rm -rf ~/.npm && npm cache clear

# Set app dir
RUN mkdir /app && chown angularexample:angularexample /app
WORKDIR /app

# Run as user
USER angularexample

# Expose the port
EXPOSE 3000
