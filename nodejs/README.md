# Quickstart

**Prerequisite**
- source code for your `node.js` project (e.g. `server.js`, `package.json`, etc.)

**Containerizing your `node.js` app:**
1. Specify `Dockerfile`: let docker know how to run your app.
    ```Dockerfile
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
    ```
    where `FROM node:12.18.1` basically downloads an image prebuilt for `node` applications from the dockerhub, and the rest of 2.the commands setups your project in a container and instructs `docker` how to run it (when a container starts)

2. build the image:
    ```bash
    docker build --tag node-docker .
    ```
    which tells docker to read from the dockerfile located at `.`, and build an image with the name/tag `node-docker`.

    If successful, you can see your image listed using the `docker images` command

3. start your container with your services!
    ```bash
    docker run -d --publish 8000:8000 --restart always --name nodejs_server node-docker
    ```
    where:
    - `-d` means to run in `detached` mode, i.e., run in background
    - `--publish 8000:8000` defines port mapping `host_port:container_port`
    - `--restart always` specifies the restart strategy in case things go wrong
    - `--name nodejs_server` the name of the container (which you can later see via `docker ps`)
    - `node-docker` is the name of the image you built in step 2

4. access your service via `curl <server_ip or localhost>:8000`!