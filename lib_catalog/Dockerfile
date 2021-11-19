FROM python:3.10-alpine as builder
ENV PYTHONBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1
WORKDIR /app

# no wheel for psycopg2-binary for python3.10 so it will be built from source
# install psycopg2 dependencies
RUN apk update \ 
    && apk add --no-cache --virtual build-deps gcc python3-dev musl-dev \
    && apk add postgresql-dev
RUN pip install --upgrade pip
COPY requirements.txt .
RUN pip install -r requirements.txt

FROM python:3.10-alpine
RUN apk update && apk add --no-cache libpq
ENV directory=/usr/local/bin
COPY --from=builder ${directory} ${directory}
ENV directory=/usr/local/lib/python3.10/site-packages
COPY --from=builder ${directory} ${directory}
COPY . .
EXPOSE 8000
CMD python manage.py migrate && python manage.py runserver 0.0.0.0:8000

