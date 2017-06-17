# mainframer-docker
Mainframer setup in docker to easily deploy it on all powerful servers

In order to build the docker image run following command `docker build -t mainframer-docker .`
  * The docker image is setup to build go, clang, gcc, buck, rust, gradle and gradle android projects. If you want to make your docker image smaller you can comment out what you don't need in the Dockerfile.

  To run the docker image run `docker run -d -p 2222:22 mainframer-docker`
  Run `ssh root@localhost -p 2222` to ssh to the docker container.
