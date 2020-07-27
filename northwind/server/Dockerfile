# this image will be based on Node v14
FROM node:14

ENV APP_DIR=/app APP_PORT=3000

ENV DB_USER=root DB_PASSWORD=changeit

# create and cd into APP_DIR
# mkdir /app
# cd /app
WORKDIR ${APP_DIR}

# copy the file from fortune into /app
# ADD local image
ADD main.js .
ADD package.json .
ADD package-lock.json .
# copy the directories
ADD config config
ADD public public
ADD views views

# install the dependencies
RUN npm install

# Add healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1

# the port the application is exposing
EXPOSE ${APP_PORT}

# run the application
ENTRYPOINT ["node", "main.js"]