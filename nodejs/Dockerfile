FROM node:12.18.1
 
WORKDIR /app

### lazy version: just copy over everything from current location 
COPY . .

### full version: just copy over the necesary source code
# COPY package.json package.json
# COPY package-lock.json package-lock.json
# RUN npm install
# COPY server.js
 
CMD [ "node", "server.js" ]
