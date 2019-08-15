FROM node:8

# Home directory for Node-RED application source code.
RUN mkdir -p /usr/src/node-red

# User data directory, contains flows, config and nodes. Add /.npm to enable loading stuff later on.
RUN mkdir /data /.npm

WORKDIR /usr/src/node-red

# Add node-red user so we aren't running as root.
RUN useradd --home-dir /usr/src/node-red --no-create-home node-red \
    && chown -R node-red:node-red /data \
    && chown -R node-red:node-red /usr/src/node-red

# package.json contains Node-RED NPM module and node dependencies
COPY package.json /usr/src/node-red/
RUN npm install

# Fix rights so that we don't expect fixed user.
RUN chgrp -R 0 /data /.npm /usr/src/node-red && \
    chmod -R g=u /data /.npm /usr/src/node-red  

# Fix rights so that we don't expect fixed user.
RUN chgrp -R 0 /data /.npm /usr/src/node-red && \
    chmod -R g=u /data /.npm /usr/src/node-red  

# User configuration directory volume
EXPOSE 1880

# Environment variable holding file path for flows configuration
ENV FLOWS=flows.json
ENV NODE_PATH=/usr/src/node-red/node_modules:/data/node_modules

CMD ["npm", "start", "--", "--userDir", "/data"]
