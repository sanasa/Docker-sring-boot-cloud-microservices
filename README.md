# Microservices with spring boot, cloud and Docker

### Docker container for discovery-service (PORT 8761 ) : 

```sh
$ sudo docker pull springcloud/eureka

```

```sh
$ sudo docker run -it -p 8761:8761 springcloud/eureka
```
You should get the following output : 

* ![capture du 2017-12-04 19-40-16](https://user-images.githubusercontent.com/11822424/33575267-5802ee3a-d93c-11e7-8f97-d6f35ad743f9.png)

And check http://172.17.0.2:8761/ :

* ![capture du 2017-12-04 19-42-06](https://user-images.githubusercontent.com/11822424/33574934-45c4cfe6-d93b-11e7-9e2a-93534fa30b59.png)

### Docker container for product-service (PORT 8081 ) :

* Modify pom.xml with a personnalized name of the jar generated after install : 

![capture du 2017-12-04 19-18-02](https://user-images.githubusercontent.com/11822424/33575114-dfc6b28a-d93b-11e7-93dd-75c77faf8e86.png)

* Create at the root of the project a Dockerfile with this content :

* ![capture du 2017-12-04 19-01-00](https://user-images.githubusercontent.com/11822424/33575173-0a747d3c-d93c-11e7-906a-270556fe8593.png)

* Add two files instead of application.properties: application.yml and bootstrap.yml and put the following content :

* ![capture du 2017-12-04 19-55-29](https://user-images.githubusercontent.com/11822424/33575512-2d63a10a-d93d-11e7-8687-f761a1105b7e.png)

* The structure of the project is than : 

* ![capture du 2017-12-04 19-53-53](https://user-images.githubusercontent.com/11822424/33575856-4695431c-d93e-11e7-9719-29c5f7b78ed7.png)

* Run the maven commands clean and install :

* ![capture du 2017-12-04 19-20-24](https://user-images.githubusercontent.com/11822424/33575168-03d5c8e6-d93c-11e7-8f08-056b995045ee.png)

* A jar file will be generated under target :

![capture du 2017-12-04 19-22-24](https://user-images.githubusercontent.com/11822424/33575228-3d5ecd10-d93c-11e7-8256-e8db84470965.png)

* Open the command line from the root of your project and build your image :

```sh
$ sudo docker build -f Dockerfile -t docker-product-spring-boot
```

### Docker container for config-service (PORT 8888 ) : 

* Follow the same steps and add the following content to the application.yml and bootstrap.yml : 

* ![capture du 2017-12-04 19-57-18](https://user-images.githubusercontent.com/11822424/33575640-99b3dc8a-d93d-11e7-995f-d149d4404413.png)

```sh
$ sudo docker build -f Dockerfile -t docker-config-spring-boot .
```

* ![capture du 2017-12-04 21-55-41](https://user-images.githubusercontent.com/11822424/33575729-e6b06d6e-d93d-11e7-97ff-0790edf16880.png)

* Detect the name of the discovery-service container in order to link it the current image :

```sh
$ sudo docker run -it --link agitated_ride:discov -p 8888:8888 docker-config-spring-boot
```

### Run product-service several instances : 

* Type those two commands like so : 

* ![capture du 2017-12-04 22-02-43](https://user-images.githubusercontent.com/11822424/33576061-ee766098-d93e-11e7-8da0-c3f60af973d1.png)

* You should get the following output :

* ![capture du 2017-12-04 22-04-24](https://user-images.githubusercontent.com/11822424/33576134-271c275c-d93f-11e7-955b-4fca8a9140e5.png)

* Run the second instance of product-service ( port 8082 ) : 

```sh
$ sudo docker run -it --link affectionate_newton:config --link agitated_ride:disc -p 8082:8082 docker-product-spring-boot

```

* Run the third instance of product-service (port 8083 ) : 

```sh
$ sudo docker run -it --link affectionate_newton:config --link agitated_ride:disc -p 8083:8083 docker-product-spring-boot

```

* Go to http://172.17.0.2:8761/ you should see : 

* ![capture du 2017-12-04 22-11-03](https://user-images.githubusercontent.com/11822424/33576416-0adec2ce-d940-11e7-8d54-6acbcbc4bc48.png)

### Docker container for proxy-service ( port 9999 ) : 

* Modify the content of application.yml and bootstrap.yml : 

* ![capture du 2017-12-04 20-27-23](https://user-images.githubusercontent.com/11822424/33576490-4487937a-d940-11e7-800a-16b47203bfad.png)

* Build and run the image : 

```sh
$ sudo docker build -f Dockerfile -t docker-proxy-spring-boot
```

* ![capture du 2017-12-04 22-15-57](https://user-images.githubusercontent.com/11822424/33576622-bad329c2-d940-11e7-8bcb-80b18b9471e1.png)


```sh
$ sudo docker run -it --link agitated_ride:disc --link affectionate_newton:conf -p 9999:9999 docker-proxy-spring-boot
```
* Go to http://172.17.0.2:8761/ you should see the proxy container registered : 

* ![capture du 2017-12-04 22-17-26](https://user-images.githubusercontent.com/11822424/33576686-f6787810-d940-11e7-8df4-fd306e8d95d5.png)

### Finally : 

* To test, the rest api of product in the microservice architecture head to http://172.17.0.7:9999/product-service/messages :










