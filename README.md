# Spring security authentication microservice
---

This example uses spring security to create an authentication endpoint that returns a JWT. It has two endpoints that are not authenticated, *sign-up* and a *login*, and a *test* endpoint for testing the authentication. The generated JWT can be used in the other microservices for the messaging application.

How to start the application
---

1. To create a MySQL docker container: `docker run --name=mysql -p 3306:3306 -d mysql/mysql-server:latest`
1. To change the generated password:
  
  `docker logs mysql 2>&1 | grep GENERATED`
  
  `docker exec -it mysql mysql -uroot -p'<output from previous step>'`
  
  `ALTER USER 'root'@'localhost' IDENTIFIED BY '<some password>';`
1. To create another user and grant previleges:
  
  `CREATE USER 'sec'@'%' IDENTIFIED BY 'spassword';`
  
  `CREATE DATABASE db_example CHARACTER SET utf8 COLLATE utf8_bin;`
  
  `GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER,INDEX on db_example.* TO 'sec'@'%' WITH GRANT OPTION;`
  
  `flush privileges;`

Testing
---

Create an user by sending a POST with username, password and displayName to the sign-up endpoint. Then login by sending a POST with username and password to the login endpoint. You'll get a JWT in the response. Finally, to test, send a GET request to the test endpoint, passing the Authorization header in the format `Bearer <JWT>`





