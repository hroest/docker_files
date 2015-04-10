FROM ubuntu:12.04

RUN apt-get -y update
RUN apt-get -y install python python-dev python-setuptools
RUN apt-get -y install g++ make 

# RUN virtualenv pyprophet
# RUN cd pyprophet
# RUN source pyprophet/bin/activate
# 
# RUN source pyprophet/bin/activate && pip install --upgrade pip
# RUN source pyprophet/bin/activate && easy_install -U distribute
# RUN source pyprophet/bin/activate && pip install numpy
# RUN source pyprophet/bin/activate && pip install matplotlib
# RUN source pyprophet/bin/activate && pip install pyprophet
# 

RUN easy_install pip
RUN pip install --upgrade pip
RUN easy_install -U distribute
RUN pip install numpy
RUN apt-get build-dep -y python-matplotlib
RUN pip install matplotlib
RUN apt-get build-dep -y python-scipy
RUN pip install pyprophet

