# Capas de las imágenes

```
docker image history alpine

echo "console.log(\"version imagen v0.2\");" >> index.js

docker image build -t hello:v0.2 .

docker image ls

docker container run hello:v0.2

docker image history hello:v0.2 
```



```
docker image inspect alpine

docker image inspect --format "{{ json .RootFS.Layers }}" alpine

docker image inspect --format "{{ json .RootFS.Layers }}" hello:v0.2
```

