# Did you know?


The absolute basics

```
 docker run -ti alpine sh
```

---


set an environmental variable `DOCKER_USER_ID`

used by all the  k8s-mastery stuff


git@github.com:bryanhuntesl/k8s-mastery.git

---

```bash
yum update -y && yum -y install \
git \
jansson \
jansson-devel \
make \
gcc \
docker \
vim \
emacs \
kubernetes-master \
kubernetes-client \
kubernetes
```

```
service docker start
```
---

digital ocean user-data equivalent

```

#cloud-config
package_update: true

#cloud-config
package_upgrade: true

#cloud-config
packages:
  - git
  - jansson
  - jansson-devel
  - make
  - gcc
  - docker
  - vim
  - emacs
  - kubernetes-master
  - kubernetes-client
  - kubernetes



---

Some tricks

---


plotnetcfg

```
git clone https://github.com/bryanhuntesl/plotnetcfg.git
cd plotnetcfg/
make
./plotnetcfg
```





docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock nate/dockviz

https://github.com/bryanhuntesl/dockviz




```
cd k8s-mastery/sa-frontend

export DOCKER_USER_ID=bryanhuntesl

docker build -f Dockerfile -t $DOCKER_USER_ID/sentiment-analysis-frontend .
```

---


```
docker run \
  -ti \
  --name devtest \
  --mount type=bind,source="$(pwd)",target=/work \
  centos:7
```

yum update -y 

---

from another terminal 

docker commit      


❯ docker commit devtest devtestv1
sha256:456bd44221fe7b8e90339f7fb7664c417de7e69b9b2d324b4b69fc10dbdf9d1f


exit the container 

```
docker run \
-ti \
--name devtestv2 \
--mount type=bind,source="$(pwd)",target=/work \
devtestv1
```

```
yum -y install epel-release
yum -y install npm maven python-pip
```

```
❯ docker commit devtestv2 devtestv2
sha256:af4ccff5543e1c1fbdf8d5c0200cef774ddb73eee85456a531586f12069d9f48
```


Inside the container : 

```
cd /work/sa-webapp/
mvn package
```

```
❯ docker commit devtestv2 devtestv3
sha256:f5a524ebaf73005ec644efa7fab86955a045ff9d2d0943ca494044b0938ad912
```

on the host 

```
/bryanhuntesl/k8s-mastery/sa-webapp master*
❯ find . | grep jar$
./target/sentiment-analysis-web-0.0.1-SNAPSHOT.jar
```


on the container 
```
cd /work/sa-frontend
npm install   
```
omg - npm/node is such a shitheap 

commit the container - I don't want to do that again.. 

```
❯ docker commit devtestv2 devtestv4
sha256:a3ee89c8f38c54dc4bc94e99024c5f52f472c47c09ca63aa8dcc5a239fdc2aba
```

Oh no... yet more npm crap 

```
npm run build
```

```
[root@e9bddf049c64 sa-frontend]# npm run build

> salogic-front@0.1.0 build /work/sa-frontend
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  73 KB  build/static/js/main.7bd4a5f6.js
  356 B  build/static/css/main.6469d74d.css

The project was built assuming it is hosted at the server root.
You can control this with the homepage field in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage" : "http://myname.github.io/myapp",

The build folder is ready to be deployed.
You may serve it with a static server:

  yarn global add serve
  serve -s build

Find out more about deployment here:

  http://bit.ly/2vY88Kr

[root@e9bddf049c64 sa-frontend]#

```

And commit the container ... again . I don't want to do that twice.

```
❯ docker commit devtestv2 devtestv5
sha256:ede9c447007a899a1663f6f2dba81a11075ebac1363bf388f3cbbd58df803ff9
```

At this stage I need to restart the container , well actually start a container from the images I created of it.


```
❯ docker run \
  -ti \
  --name devtestv6 \
  -p 3000:3000 \
  --mount type=bind,source="$(pwd)",target=/work \
  devtestv5
```

```
cd /work/sa-frontend/













