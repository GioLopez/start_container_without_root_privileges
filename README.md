# Run container without root privileges

By default containers run with root privileges, it is a big security mistake to run like this, one of the best practice that OWAS recommend is to avoid this practice, to achive that, follow the next steps.

## 1. Create a docker file

```
vim Dockerfile
```

## 2. Add the following information in Dockerfile file

```
FROM centos:7
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
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
docker run --rm my_image:1
```

It will let you in the container, you could check with id command which user is the container using, the working dir, the file inside /home/apps directory

## 5. Validate file mi-archivo.txt file in /home/apps/

```
docker run --rm my_image:1 cat /home/apps/mi-archivo.txt
```

That's all folks, thanks for visiting!
