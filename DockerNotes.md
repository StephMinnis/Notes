Docker Notes
------------------






Maintenance
One liner to stop / remove all of Docker containers:
  docker stop $(docker ps -a -q)
  docker rm $(docker ps -a -q)
  
  Remove all non-running container
  sudo  docker ps -a | grep 'Exited' | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm
  
  ssh to the container
  docker exec -it e2a560cc4947 /bin/bash
  
  build image
  docker build -t your_image_name .
  
  run container 
  sudo docker run -it -p 80:80 image_name
  
  