 ######     ###    ##    ## ########  ########   #######  ##     ##
##    ##   ## ##   ###   ## ##     ## ##     ## ##     ##  ##   ##
##        ##   ##  ####  ## ##     ## ##     ## ##     ##   ## ##
 ######  ##     ## ## ## ## ##     ## ########  ##     ##    ###
      ## ######### ##  #### ##     ## ##     ## ##     ##   ## ##
##    ## ##     ## ##   ### ##     ## ##     ## ##     ##  ##   ##
 ######  ##     ## ##    ## ########  ########   #######  ##     ##

FROM ubuntu

# Install some custom upstream packages
RUN apt-get update
RUN apt-get install -y \
  cowsay fortune \
  curl

# Load the Dockerfile *into* the container (for `dump' script)
ADD Dockerfile /

# Install custom scripts
ADD scripts/* /usr/local/bin/
RUN chmod 755 /usr/local/bin/*

ENV SPRUCE_VERSION=1.0.1 \
    JQ_VERSION=1.5

# spruce
RUN curl -L >spruce.tar.gz https://github.com/geofffranks/spruce/releases/download/v${SPRUCE_VERSION}/spruce_${SPRUCE_VERSION}_linux_amd64.tar.gz \
  && tar -xvzf spruce.tar.gz \
  && mv spruce_${SPRUCE_VERSION}_linux_amd64/spruce /usr/bin/spruce \
  && rm -rf spruce.tar.gz spruce_${SPRUCE_VERSION}_linux_amd64

# jq
RUN curl -L >/usr/bin/jq https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 \
  && chmod 755 /usr/bin/jq

# Set up $PATH properly
ENV PATH="$PATH:/usr/games"
