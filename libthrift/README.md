# how to build it

clone repo and apply patchset

```sh
git clone git@github.com:apache/thrift.git
cd thrift
git checkout 0.13.0
git apply patch13.diff
cd ..
```

run ubuntu 20.04 to build it

```sh
sudo docker rm thrift-build
sudo docker run -it --name thrift-build -v $(pwd)/thrift:/thrift ubuntu:20.04

apt-get update
apt-get install -y openjdk-13-jre-headless openjdk-13-jdk make bison flex gcc cmake make g++
cd /thrift/compiler/cpp
mkdir cmake-build
cd cmake-build
cmake ..
make
cp bin/thrift ..
cd ../../../lib/java
./gradlew
cp build/libs/libthrift-0.13.0-SNAPSHOT.jar ../../libthrift-0.13.0.jar
exit

sudo docker cp thrift-build:/thrift/libthrift-0.13.0.jar .
sudo docker rm thrift-build
```

use it.
