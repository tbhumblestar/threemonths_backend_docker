# FROM python:3.9-alpine #alpine은 git이 없음!
FROM python:3.9
WORKDIR /home/threemonths
ARG GIT_ACCESS_TOKEN
RUN git clone https://${GIT_ACCESS_TOKEN}@github.com/tbhumblestar/threemonths_backend.git
WORKDIR /home/threemonths/threemonths_backend

COPY secret_settings.py .

RUN pip3 install -r requirements.txt

RUN pip3 install gunicorn

CMD ["gunicorn", "--bind","0.0.0.0:8000", "threemonths.wsgi:application"]
#CMD ["nohup", "gunicorn", "--bind=0.0.0.0:8000", "threemonths.wsgi","&"]

EXPOSE 8000