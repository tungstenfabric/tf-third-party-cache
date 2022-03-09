# how to build it

clone repo and apply patchset

```sh
git clone git@github.com:apache/thrift.git
cd thrift
git checkout 0.13.0
git apply patch13.diff
cd ..
```

run ubuntu 20.04 container to build it

```sh
sudo docker run -it --rm -v $(pwd)/thrift:/thrift ubuntu:20.04

export DEBIAN_FRONTEND=noninteractive
apt-get update && apt-get install -y openjdk-11-jdk make bison flex gcc cmake make g++

cd /thrift/compiler/cpp
mkdir cmake-build
cd cmake-build
cmake ..
make
cp bin/thrift ..
cd ../../..

cd lib/java
./gradlew -Prelease=true
cp build/libs/libthrift-0.13.0.jar ../../libthrift-0.13.0.jar
exit
```

use it from thrift/libthrift-0.13.0.jar
