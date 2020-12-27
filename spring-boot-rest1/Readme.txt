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
