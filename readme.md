# Dockerfile


```
FROM  ubuntu:14.04
RUN sudo apt-get update
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list.d/pgdg.list
RUN sudo apt-get install -y -q wget
RUN wget --no-check-certificate  --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
RUN sudo apt-get update
RUN apt-get install -y -q postgresql-server-dev-9.4
RUN apt-get install -y -q python-pip
RUN sudo apt-get install -y -q python-dev
RUN sudo pip install pip --upgrade
RUN apt-get install -y -q git
RUN git clone https://github.com/cai-yang/neurorehab.git neurorehab
RUN echo "PATH="$/etc/postgresql/9.4/main:$PATH"" >> ~/.profile
RUN sudo pip install -r neurorehab/requirements.txt
EXPOSE 8000
CMD python neurorehab/manage.py runserver 0.0.0.0:8000
```


```
sudo docker build -t your-image-name .
```
Don't miss the last "." in the command.


```
sudo docker run -d -p 8000:8000 your-image-name
```
Run it in background and go to http://127.0.0.1:8000/ to browse.
