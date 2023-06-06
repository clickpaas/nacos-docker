#build nacos source code :
mvn -Prelease-nacos -DskipTests -Dcheckstyle.skip=true clean install

#copy gz file here:
cp nacos/distribution/nacos-server-2.1.2.tar.gz nacos-docker/build/nacos-server-2.1.2.tar.gz

#push docker
cd build
make push

