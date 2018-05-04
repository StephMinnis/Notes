## Docker Notes
---

#### Useful Commands

**Show all continers**
>Docker ps -a

**Connect to shell on running container**
>Docker exec -it e2a560cc4947 bash

**Run container **
>Docker run -it -d 80:80 image_name

#### Maintenance
One liner to stop / remove all of Docker containers:
  >docker stop $(docker ps -a -q)
  >docker rm $(docker ps -a -q)
  
**Remove all non-running container**
>sudo  docker ps -a | grep 'Exited' | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm
  
 **Build image**
>docker build -t your_image_name .
  

  