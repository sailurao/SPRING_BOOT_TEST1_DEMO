This project serves as API SERVER, and uses the Custom Mysql docker image  (naga1972/mycustom_sql_img) for backend database.
The database container name should be mysql-dev-server.  It also uses the ReactJs example that is posted here.
All the three Docker images can be pulled to containers to work together using below docker-compose.yml file.





DOCKERIZING INSTRUCTIONS
------------------------------------------------------------------------------------------------------------

Reference: https://github.com/rajasekharreddybusireddy/spring-boot-docker-mysql

1. mvn clean package

   Note: if you get mysql exceptions, then dont forget to comment test annotation @Test 

2. docker pull mysql:5.6

3. docker run --name=mysql-dev-server -e MYSQL_ROOT_PASSWORD=Java2020 -e MYSQL_USER=test -e MYSQL_PASSWORD=Java2020 -e MYSQL_DATABASE=test -d mysql

4. docker pull phpmyadmin/phpmyadmin

5. docker run --name myphpadmin -d --link mysql-dev-server:db -p 8081:80 phpmyadmin/phpmyadmin

6. create table using phpmyadmin webapp at http://localhost:8081
  and then execute below query

use test;
CREATE TABLE `user` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `firstName` VARCHAR(45) NOT NULL,
  `lastName` VARCHAR(45) NULL,
  `age` INT NULL,
  `salary` BIGINT NULL,
  `username` VARCHAR(45) NULL,
  `password` VARCHAR(255) NULL,
  PRIMARY KEY (`id`));


INSERT INTO  user(firstName, lastName , age , salary , username,password )  values("Rama", "Taraka" ,  25 ,  10000 ,  "ramar" ,  "1234");

7. docker build -f Dockerfile -t users-mysql-app .
8.    docker run -p 8080:8080 --name final-app -d --link mysql-dev-server:mysql users-mysql-app 





--------------------------------------------------------------------------------------
   docker-compose.yml
------------------------------------------------------------------------
version: '3.2'

services:
   mysql-dev-server:
      image: naga1972/mycustom_sql_img
      container_name: mysql-dev-server
      restart: always
      ports:
       - '3306:3306'
      environment:
        MYSQL_ROOT_PASSWORD: Java2020


   mySpringBootRest1:
      depends_on:
       - mysql-dev-server
      image: naga1972/spring-boot-rest1-img
      container_name: mySpringBootRest1
      restart: always
      ports:
       - '8080:8080'
      environment:
        PMA_HOST: mysql-dev-server

   phpmyadmin:
      depends_on:
       - mysql-dev-server
      image: phpmyadmin/phpmyadmin
      container_name: phpmyadmin
      restart: always
      ports:
       - '8081:80'
      environment:
        PMA_HOST: mysql-dev-server


   react-example1-app:
      image: naga1972/react-example1
      container_name: react-example1-app
      restart: always
      ports:
       - '3000:3000'
   














