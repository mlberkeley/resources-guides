# Building a docker container for machine learning
This repo guides you through building a docker container for machine learning. Specifically, we're going to build a container to do fast style transfer with an already existing codebase.

All docker containers are built from Dockerfiles. They specify what needs to be done to build the container. Once a dockerfile has been created, you can build it with `docker build`.

docker build -t $USERNAME/$CONTAINER_NAME:$TAG
e.g. docker build -t matthewsoh/fast-style-transfer-example:latest-gpu

Open the provided Dockerfile to learn how it's written.

Once the Dockerfile has been finished, you can build the container and then execute it with `docker run`.

docker run -v $LOCAL_DEST:$CONTAINER_DEST -it $CONTAINER_NAME $ADDITIONAL_ARGUMENTS
  -v is used to specify a bound volume. In this case, we're binding /notebooks/img-out, the output folder, to our present working directory $pwd.

e.g. docker run -v $(pwd):/notebooks/img-out -it fast-style-transfer-example --checkpoint ./models/wave.ckpt --in-path img-in --out-path /notebooks/img-out

## Pushing to dockerhub
This requires an account on dockerhub. Once you have created this account, you can login and push the built docker container as follows.

```
docker login
docker build -t $USERNAME/fast-style-transfer-example:latest-gpu .
docker push $USERNAME/fast-style-transfer-example:latest-gpu
```
