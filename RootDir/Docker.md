### Docker command

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
<Host Port>:<Container Port>  
- docker run --name "ContainerName2" --network "NetworkName" "ImageName":"tag"

- docker port "ContainerName"

### DockerFile

#### .dockerignore
*.cpp
.git
.img

#### docker create image using DockerFile
- docker build --tag "ImageName" ./

FROM "ImageName":"tag"
>> 기반이 되는 이미지를 설정  
여러가지 FROM 사용 가능, --tag 태그 적용했다면 맨 마지막 FROM만

MAINTAINER "Auther Info"

RUN "bash command"
>> FROM에서 설정한 이미지에서 bash command 실행  
RUN apt-get update  
RUN apt-get upgrade  
RUN apt-get install mysql  
RUN git clone ...  
RUN ["apt-get", "update"]  
RUN ["git", "clone", "https://github.com/..."]  

CMD "bash command"
>> 컨테이너 run, start 할 때 실행되는 command  
CMD ["python3", "server.py"]

ENTRYPOINT ["echo" "Hello"]
>> 컨테이너를 run할 때 "echo hello" 구문을 추가해줬다면 CMD는 실행 x, ENTRYPOINT는 실행 o  

EXPOSE 80
EXPOSE 443
EXPOSE 80 443
>> 호스트와 연결할 포트를 설정 / docker run -p 옵션과는 다른 것

ENV "환경변수" "값"
>> ENV path /var/lib/tomcat  
CMD echo $path  
docker run -e path=/var/lib 도 가능

ADD "Original File path" "path in docker Container (Image)"
>> ADD /lib/text.txt /root/text.txt (o)  
ADD ../var/lib/text.txt /root/text/txt (x) (상위 폴더 불가능)  
ADD /lib/ /root/ (디렉토리 전체 가능)  
ADD URL /root/text.txt가능


COPY "Original File path" "path in docker Container (Image)"
>> ADD와 달리 압축 해제 안함, URL 사용 불가능  

VOLUME "path"
VOLUME ["path1", "path2"]
>> 컨테이너에 데이터 저장하지 않고 호스트 내의 디렉토리에 저장  
호스트 내의 위치를 지정하려면 docker run 옵션에서 지정해야 함.  
docker run -v "host dir":"container dir"  
docker run -v /project/pp:/pp

USER root
USER "username"
>> bash command 사용할 때 유저를 정함 (RUN, CMD, ...)

WORKDIR "path"
>>bash command 사용할 때 기본 디렉터리를 정함.  

>> RUN cd /var/lib/pythonServer python3 server.py (o)  
>> RUN python3 test.py (x) -> 각 구문이 독립적으로? 실행됨으로 최상위 디렉토리로 다시 돌아감.  

>> WORKDIR /var/lib/pythonServer  
>> RUN python3 server.py (o)  
>> RUN python3 test.py (o)

ONBUILD RUN echo hello (ImageName: onbuildImage)
>> 자신을 컨테이너로 만들때는 실행되지 않고 자신을 상속하는 컨테이너가 실행될 때 구문이 실행된다.  
ex) FROM onbuildImage 구문을 가지는 이미지가 컨테이너에 실리면 echo hello


