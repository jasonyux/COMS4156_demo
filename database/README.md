# Quickstart

Setting up a `mysql` or `redis` database is a bit more complicated than the other two. Why? Because you will need to be careful of:
- volume mounts: you don't want to lose your all your data after a single container restart, which unfortunately is the default behavior of containers (so that they are really lightweight!)
- networking: you may need to configure your container's network configuration for security concerns


See the following for more details
- https://github.com/jasonyux/devfest2021-dockerPlusSpring for a (not so quick) quickstart.
- https://www.baeldung.com/ops/docker-mysql-container