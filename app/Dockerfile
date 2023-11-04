# pull official base image
FROM python:3.11.4-slim-buster

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1


RUN apt-get update \
    && apt-get -y install libpq-dev gcc \
    && apt-get install -y netcat \
    && pip install psycopg2


COPY ./requirements.txt .
RUN pip install -r requirements.txt


# copy entrypoint.sh
COPY ./entrypoint.sh /usr/src/app/
RUN sed -i 's/\r$//g' /usr/src/app/entrypoint.sh
RUN chmod +x /usr/src/app/entrypoint.sh


# copy project
COPY . .

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]