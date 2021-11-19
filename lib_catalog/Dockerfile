FROM python:3.10-slim
ENV PYTHONBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1
WORKDIR /app

# install psycopg2 dependencies
RUN apt-get update \
    && apt-get -y install libpq-dev gcc

RUN pip install --upgrade pip
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 8000
CMD python manage.py migrate && python manage.py runserver 0.0.0.0:8000

