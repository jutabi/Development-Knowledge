- docker pull ubuntu:16.04

- docker images

- docker run -i -t --name "ContainerName" "ImageName":"tag"

- Ctrl + p , Ctrl + q = Exit (keep container processing)

- docker stop, start, attach "ContainerName"

- docker ps (-a)

- docker rm "ContainerName"

- docker rmi "ImageName"

- docker tag "ImageName":"tag" "ECR_Address/"ImageName":"tag"
- docker push "ECR_Address"/"ImageName":"tag"
- docker pull "ECR_Address"/"ImageName":"tag"

- docker network create "NetworkName"
- docker run --name "ContainerName1" -p 80:80 --network "NetworkName" "ImageName":"tag"
- docker run --name "ContainerName2" --network "NetworkName" "ImageName":"tag"