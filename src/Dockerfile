FROM ubuntu:latest

# Install python3-pip
RUN apt-get update -y \
	&& apt-get install -y python3-pip \
	libgl1-mesa-glx \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y libgtk2.0-dev \
	&& rm -rf /var/lib/apt/lists/*

# integrate only necessary files
RUN mkdir app
RUN mkdir app/template
RUN mkdir app/model
RUN mkdir app/predict
RUN mkdir app/preprocessing

COPY template app/template
COPY model/model_final.h5 /app/model
COPY preprocessing/preprocess.py /app/preprocessing
COPY app.py /app
COPY Procfile /app
COPY requirements-docker.txt /app

WORKDIR /app
RUN pip3 install -r requirements-docker.txt

# files paths in py scripts will be parsed relative to WORKDIR
WORKDIR /

# library/module imports are relative to PYTHONPATH
# (defaults to app.py location)
#CMD export PYTHONPATH="${PYTHONPATH}:/" ; python3 source/app.py

CMD python3 app/app.py