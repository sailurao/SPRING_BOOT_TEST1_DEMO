It needs Mysql Database "test", root, password:Java2020.

Also It looks for the table "user", with the below schema

CREATE TABLE `user` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `firstName` VARCHAR(45) NOT NULL,
  `lastName` VARCHAR(45) NULL,
  `age` INT NULL,
  `salary` BIGINT NULL,
  `username` VARCHAR(45) NULL,
  `password` VARCHAR(255) NULL,
  PRIMARY KEY (`id`));


