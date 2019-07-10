# Start container without root privileges

## 1. Create a docker file

```
vim Dockerfile
```

## 2. Add the following information in Dockerfile file

```
FROM centos:7
RUN useradd apps
USER apps
```

Dockerfile indicate that conteiner will user Centos 7 and will RUN with user apps

## 3. Build Centos 7 image with user apps

```
docker build -t my_image:1 .
```

NOTE: Need to be sure that docker is running

## 4. Run the folowwing command to check that container run without user

```
docker run --rm my_image:1 id
```

That's all, thanks for visiting!
