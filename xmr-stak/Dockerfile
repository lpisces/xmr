FROM centos:7

RUN yum update -y 

RUN yum install centos-release-scl epel-release -y
RUN yum install cmake3 devtoolset-7-gcc* hwloc-devel libmicrohttpd-devel openssl-devel make -y
#RUN /usr/bin/scl enable devtoolset-7 bash
ENV PATH $PATH:/opt/rh/devtoolset-7/root/usr/bin

COPY src /tmp/src

RUN mkdir /tmp/src/build

WORKDIR /tmp/src/build

RUN cmake3 -DCMAKE_LINK_STATIC=ON -DXMR-STAK_COMPILE=generic -DCUDA_ENABLE=OFF -DOpenCL_ENABLE=OFF ..
RUN make install

COPY ./config.txt bin/
COPY ./pools.txt bin/
COPY ./cpu.txt bin/

WORKDIR /tmp/src/build/bin
CMD ./xmr-stak
