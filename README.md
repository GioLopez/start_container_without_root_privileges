# Run container without root privileges

By default containers run with root privileges, it is a big security mistake to run like this, one of the best practice that OWAS recommend is to avoid this practice, to achive that, follow the next steps.

## 1. Create a docker file

```
vim Dockerfile
```

## 2. Add the following information in Dockerfile file

```
FROM centos:7
RUN useradd apps
USER apps
WORKDIR /home/apps
ADD mi-archivo.txt /home/apps
```

Dockerfile indicate that conteiner will user Centos 7 and will RUN with user apps, with the working directory on /home/apps and ADD the file mi-archivo.txt to /home/apps/

NOTE: mi-archivo.txt need to exists before build the container

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
