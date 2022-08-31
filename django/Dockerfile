# FROM python:3.9-alpine #alpine은 git이 없음!
FROM python:3.9
WORKDIR /home/threemonths
ARG GIT_ACCESS_TOKEN
RUN git clone https://${GIT_ACCESS_TOKEN}@github.com/tbhumblestar/threemonths_backend.git
WORKDIR /home/threemonths/threemonths_backend

#현재 서버의 경로에 있는 파일을 WORKDIR로 복사
COPY secret_settings.py .

RUN pip3 install -r requirements.txt

RUN pip3 install gunicorn


CMD ["gunicorn", "--bind","0.0.0.0:8000", "threemonths.wsgi:application"]
#CMD ["nohup", "gunicorn", "--bind=0.0.0.0:8000", "threemonths.wsgi","&"]
#CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]

EXPOSE 8000


# #dockerfile
# FROM ubuntu:20.04

# RUN apt-get update
# RUN apt-get install git -y
# RUN apt-get install python3 -y
# RUN apt-get install python3-pip -y
# RUN apt-get install vim -y

# #Declaring working directory in our container
# WORKDIR /home/threemonths 

# #username과 password를 묻지 않는다.
# RUN git clone https://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@github.com/tbhumblestar/threemonths_backend.git

# WORKDIR /home/threemonths/threemonths_backend

# #현재 서버의 경로에 있는 파일을 WORDIR로 복사
# COPY secret_settings.py .

# RUN pip3 install -r requirements.txt

# RUN pip3 install gunicorn


# CMD ["gunicorn", "--bind","0.0.0.0:8000", "threemonths.wsgi:application"]
# #CMD ["nohup", "gunicorn", "--bind=0.0.0.0:8000", "threemonths.wsgi","&"]
# #CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]

# EXPOSE 8000
