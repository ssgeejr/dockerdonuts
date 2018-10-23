# dockerdonuts
Simplified java web-app creating both a standard java war (Web ARchive, webapp) and an executable jar (Java ARchive) with embedded Tomcat-7

### Clone the repository
```
git clone git@github.com:ssgeejr/dockerdonuts.git
```
or
```
git clone https://github.com/ssgeejr/dockerdonuts.git
```

### Build the code

```
cd dockerdonuts
mvn clean package
```

Once the build successfully completes  
make sure both files are available

```
[devops:dockerdonuts]$ dir docker target  
docker:  
Dockerfile  sacreddonut.jar  war-exec.manifest  war-exec.properties  

target:  
maven-archiver  sacreddonut  sacreddonut.war  
```

target/sacreddonut.war will be referenced by the tomcat Docker image. While the executable jar file, docker/sacreddonut.jar, will be used in the stand-alone Docker container  

to test the build, you can start the tomcat instance by executing:

```
java -jar docker/sacreddonut.jar
```

then point your browser to [localhost:8080](http://localhost:8080)

### Building the docker image
from the docker folder, execute the following command:
```
docker build -t sacreddonut .
```

Now start the container:
```
docker run --rm --name sdonut -p 8080:8080 -ti sacreddonut
```
then point your browser to [localhost:8080](http://localhost:8080)

Let's start tomcat and reference the war file  

```
docker run --rm --name sdonut -v ./target/sacreddonut.war:/usr/local/tomcat/webapps/sacreddonut.war -p 8080:8080 -ti tomcat
```

then point your browser to [localhost:8080/sacreddonut/](http://localhost:8080/sacreddonut/)













..
