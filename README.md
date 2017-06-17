# mainframer-docker
Mainframer setup in docker to easily deploy it on all powerful servers

# Build server
In order to build the docker image run following command `docker build -t mainframer-docker .`
  * The docker image is setup to build go, clang, gcc, buck, rust, gradle and gradle android projects. If you want to make your docker image smaller you can comment out what you don't need in the Dockerfile.

  To run the docker image run `docker run -d -p 2222:22 mainframer-docker`.
  Run `ssh root@localhost -p 2222` to ssh to the docker container.

# Client

Beside the project specific setup we need 2 more things, an ssh-key in order to make communication between client and server easier to maintain. And a ssh config for our server.

  ```bash
  ssh-keygen -t rsa -f ~/.ssh/remote-builder -q -N ""
  #brew install ssh-copy-id
  ssh-copy-id -i ~/.ssh/remote-builder root@192.168.0.129 -p 2222

  echo -e "Host REMOTE_BUILDER \n \
             User root \n \
             HostName 192.168.0.129 \n \
             Port 2222 \n \
             IdentityFile ~/.ssh/remote-builder \n \
             PreferredAuthentications publickey \n \
             ControlMaster auto \n \
             ControlPath /tmp/%r@%h:%p \n \
             ControlPersist 1h" >> ~/.ssh/config
  ```

For android you can now just copy the mainframer folder and rename it `.mainframer` and you should be go to run ` bash ./mainframer.sh ./gradlew assembleDebug`.

**And now enjoy faster builds**
