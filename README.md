FROM ubuntu                                                            #using ubuntu as a docker base image
RUN apt-get update -y && apt-get install nginx -y && mkdir /HTML       #executing commands to update, install nginx server and create a dir named HTML
WORKDIR /HTML                                                          #while running the docker container it should open HTML dir as a working dir
RUN echo "Hellow World" >index.html                                   
COPY ./HTML/* /usr/share/nginx/html                                    #Copying the HTML dir from the host machine to the doker container
EXPOSE 80/tcp 

docker build -t newimage .                           
docker run -td --name test -p 8080:80 -v HTML:/usr/share/nginx/html newimage           # docker container in the detached mode (-d) and Nginx webserver runs on port 80
