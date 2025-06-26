FROM python:3.9
RUN apt-get update && \
    apt-get install -y python3-distutils && \
    pip install django==3.2

WORKDIR /app
COPY . .

RUN python manage.py migrate
EXPOSE 8000
CMD ["python","manage.py","runserver","0.0.0.0:8000"]


