FROM buildpack-deps:stretch

ENV HOST localhost
ENV PORT 3000

# Create app directory
RUN mkdir -p /usr/src/app
RUN apt install -y git
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
WORKDIR /
RUN git clone https://github.com/askmike/gekko.git -b stable
RUN mv gekko/* /usr/src/app/
RUN git clone https://github.com/xFFFFF/Gekko-Strategies -b master
WORKDIR /Gekko-Strategies
RUN ./install.sh /usr/src/app
WORKDIR /usr/src/app


# Install GYP dependencies globally, will be used to code build other dependencies
RUN npm install -g --production node-gyp && npm cache clean --force

# Install Gekko dependencies
RUN ls -l /usr/src/app/
RUN npm install --build-from-source --production && \
    npm install --production redis@0.10.0 talib@1.0.2 tulind@0.8.7 pg && \
    npm cache clean --force

# Install Gekko Broker dependencies
WORKDIR exchange
RUN npm install --production && \
    npm cache clean --force
WORKDIR ../

#add custom strategies



EXPOSE 3000
RUN chmod +x /usr/src/app/docker-entrypoint.sh
ENTRYPOINT ["/usr/src/app/docker-entrypoint.sh"]

CMD ["--config", "config.js", "--ui"]
