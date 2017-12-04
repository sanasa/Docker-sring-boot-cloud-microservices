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

* Run the maven commands clean and install :

* ![capture du 2017-12-04 19-20-24](https://user-images.githubusercontent.com/11822424/33575168-03d5c8e6-d93c-11e7-8f08-056b995045ee.png)

* A jar file will be generated under target :

![capture du 2017-12-04 19-22-24](https://user-images.githubusercontent.com/11822424/33575228-3d5ecd10-d93c-11e7-8256-e8db84470965.png)

* Open the command line from the root of your project and build your image :

```sh
$ sudo docker build -f Dockerfile -t docker-product-spring-boot
```










