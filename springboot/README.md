# Quickstart

**Prerequisite**
- source code for your `springboot` project
- a compiled `*.jar` executable in `target/` (e.g. after doing `mvn package`)

**Containerizing your `springboot` app:**
1. Specify `Dockerfile`: let docker know how to run your app.
    ```Dockerfile
    FROM eclipse-temurin:17-jdk-alpine
    VOLUME /tmp

    ### all you need to copy over is the compiled jar file!
    COPY ./target/*.jar app.jar
    CMD ["java","-jar","/app.jar"]
    ```
    where `eclipse-temurin:17-jdk-alpine` basically downloads an image prebuilt for `jdk-17` applications from the dockerhub, and the rest of the commands setups your project in a container and instructs `docker` how to run it (when a container starts)

2. build the image:
    ```bash
    docker build --tag springboot-docker .
    ```
    which tells docker to read from the dockerfile located at `.`, and build an image with the name/tag `springboot-docker`.

    If successful, you can see your image listed using the `docker images` command

3. start your container with your services!
    ```bash
    docker run -d --publish 8080:8080 --restart always --name springboot_server springboot-docker
    ```
    where:
    - `-d` means to run in `detached` mode, i.e., run in background
    - `--publish 8080:8080` defines port mapping `host_port:container_port`
    - `--restart always` specifies the restart strategy in case things go wrong
    - `--name springboot_server` the name of the container (which you can later see via `docker ps`)
    - `springboot-docker` is the name of the image you built in step 2

4. access your service via `curl <server_ip or localhost>:8080`!