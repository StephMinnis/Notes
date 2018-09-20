## Docker Notes



### -Useful Commands

**Connect to docker host from windows bash**
>docker -H tcp://0.0.0.0:2375
--Need to set DOCKER_HOST to that url in bashrc

**Getting windows bash to work with docker-machine**
turn on the Expose daemon on tcp;/localhost:2375 option in docker settings
in windows bash: export DOCKER_HOST=tcp://127.0.0.1:2375
To make this stick:
    >echo "export DOCKER_HOST='tcp://127.0.0.1:2375'">> ~/.bashrc
    >source ~/.bashrc

**Show all continers**
>Docker ps -a

**Connect to shell on running container**
>Docker exec -it e2a560cc4947 bash

**Run container**
>Docker run -it -d 80:80 image_name

**Check Container resources**
>Docker Stats

### -NGINX

**Create default container on port 80**
>docker run --name mynginx1 -p 80:80 -d nginx

**Test the webserver
curl http://localhost

### -Maintenance
One liner to stop / remove all of Docker containers:
  >docker stop $(docker ps -a -q)
  >docker rm $(docker ps -a -q)
  
**Remove all non-running container**
>sudo  docker ps -a | grep 'Exited' | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm
  
 **Build image**
>docker build -t your_image_name .

**Install Docker Machine**
https://docs.docker.com/machine/install-machine/#how-to-uninstall-docker-machine

**Install Docker Machine for Windows Bash**
>base=https://github.com/docker/machine/releases/download/v0.14.0 &&
>  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
>  sudo install /tmp/docker-machine /usr/local/bin/docker-machine

**Install Docker Machine in Git Bash**
>base=https://github.com/docker/machine/releases/download/v0.14.0 &&
>  mkdir -p "$HOME/bin" &&
>  curl -L $base/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe" &&
>  chmod +x "$HOME/bin/docker-machine.exe"
  
**Resources**
This site had a good tutorial on creating a LEMP stack
https://www.howtoforge.com/tutorial/dockerizing-lemp-stack-with-docker-compose-on-ubuntu/

-Needed to make sure C was shared to get containers working
# docker run --name mynginx2 --mount source=/var/www,target==/usr/share/nginx/html,readonly --mount source=/var/nginx/conf,target=/etc/nginx/conf,readonly -p 80:80 -d nginx
  