# WildFly
WildFly Application Server image

## How to deploy a WAR file
1. Create a Dockerfile with the following content:
```
FROM davimss/wildfly:X.Y.ZZ # Replace X.Y.ZZ with the WildFly version
COPY MySystem.war standalone/deployments/MySystem.war
```    
Put the Dockerfile and the *.WAR file on the same directory.

2. Call Docker to create your custom image, with the follwing command

`docker build -t my-system-image .`

3. Call Docker to create/run your container

`docker run --name my-system-container -d -p 8080:8080 my-system-image`

4. Check your container logs with the following command

`docker logs my-system-container`

5. Access your system URL with your favorite web browser: http://localhost:8080/MySystem
