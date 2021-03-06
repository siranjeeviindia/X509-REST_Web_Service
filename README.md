# X509-REST_Web_Service
A REST Web Service that provides X509 mutual certificate authentication. This web service has an HTTPS endpoint that runs through SSL certificate verification and can recieve and output data in JSON format. The X509 is handled through Spring security and a RESTful API was used to handle the GET and POST requests for the data. The server in this case has also been modified to only allow verified clients. This application can be packaged and launched through maven with the command ```mvn spring-boot:run```. You should then be able to see your successfully run web service on [https://localhost:8443/user](https://localhost:8443/user).


## RESTful API
A RESTful API uses GET to retrieve a resource, PUT to change the state of or update a resource, which can be an object, file or block, POST to create that resource; and DELETE to remove it.
```java
@RequestMapping(value = "/secured", method = {RequestMethod.GET, RequestMethod.POST}, consumes = {"application/json"})
@ResponseBody
public ResponseEntity<String> secured(@RequestBody Message m) {	
		String accountID = "999\n";
		if (m.getDid() == 1) {
		  accountID = "101\n";
		} else if (m.getDid() == 2) {
		  accountID = "102\n";
		} else if (m.getDid() == 3) {
		  accountID = "103\n";
		} else if (m.getDid() == 4) {
		  accountID = "104\n";
		} else if (m.getDid() == 5) {
		  accountID = "105\n";
		} 
		return new ResponseEntity<String>(accountID, HttpStatus.OK);
}
```

## X509 Certificate Authentication
Allow us to verify the identity of a communication peer when using the HTTPS (HTTP over SSL) protocol.
While a secure connection is established, the client verifies the server according to its certificate (issued by a trusted certificate authority). 

This is why it is also important to provide the location of the trustore and tell our server that client authentication is needed in our application.properties file. 
```
server.ssl.trust-store=**PATH**/truststore.jks
server.ssl.trust-store-password=password
server.ssl.client-auth=need
```

## Built With
* [Spring Boot](https://spring.io/projects/spring-boot) - The framework used to build this application in Java
* [Jackson Databind](https://github.com/FasterXML/jackson-databind) - Dependency used to handle JSON message as a Java object
* [Maven](https://maven.apache.org/) - Dependency management used to package and run application


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

## References
[Restful](https://spring.io/guides/gs/rest-service/) - Guide to building your own RESTful web service with Spring

[JSON](https://www.leveluplunch.com/java/tutorials/014-post-json-to-spring-rest-webservice/) - Tutorial on how JSON binds to java object

[Spring Security](https://spring.io/projects/spring-security) - Documentation for Spring Security

