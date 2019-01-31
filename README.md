# MyLearnings
useful commands list in one place

Docker installation :

Root user : sudo -s

Docker installation :curl -fsSL https://get.docker.com/ | sh

Docker most useful commands : 

To pull images from dockerhub : sudo docker pull imageName

List of images : sudo docker images

To tag images : sudo docker tag imageIddockerRegistry/imagename:latest

To push images to registry : sudo docker push dockerRegistry/imagename

To see list of containers :sudo docker ps

To see running containers :sudo docker ps -a

To remove image : sudo docker rmi imageId

To remove container :sudo docker rm –f  containerId



To remove images :

sudo docker ps -a | grep 'Exited' | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm

sudo docker ps -a | grep 'Dead' | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm

sudo docker ps -a | grep 'Created' | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm

sudo docker ps -a | awk '{print $1}' | xargs --no-run-if-empty sudo docker rm -f

sudo docker rmi $(sudodocker images -q)



Docker Registry :

Deploying a registry server

docker run -d -p 5001:5000 --restart=always --name registry -v `pwd`/data:/var/lib/registry registry:2

To stop Registry :docker stop registry

To remove registry :docker rm -v registry

To see list of images in docker registry :curl -X GET http://IpAdreess:5001/v2/_catalog

To go inside container /image :sudo docker exec -i -t imageId/bin/bash

Gitbucket

Docker - Gitbucket  installation steps :

=============================================================

docker pull sken/gitbucket

sudo mkdir -p /opt/data/gitbucket

sudo docker run -d -p 8080:8080 --name gitbucket -v /opt/data/gitbucket:/gitbucketsken/gitbucket

To remove GitBucket : sudo docker rm -f gitbucket

GIT commands :

gitinit
git add
git commit  -m “first commit”
git remove add origin  http://ipAddress/git/root/FolderName.git
git push –u origin master


Nginx

sudo docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx

sudo docker run --name docker-nginx -p 80:80    -v ~/docker-nginx/html:/usr/share/nginx/html -v ~/docker-nginx/default.conf:/etc/nginx/conf.d/default.confnginx

go to ~/docker-nginx   folder and replace default.conf file with below file .

server {
location /web-tomcat {
proxy_pass http://host:port/;
proxy_intercept_errors on;
proxy_set_header Host $http_host;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
location ~ \.(gif|jpg|png)$ {
root /data/images;
}
location / {
proxy_pass http://host:port;
}

}

Then

sudo docker restart docker-nginx

~/docker-nginx/default.conf

