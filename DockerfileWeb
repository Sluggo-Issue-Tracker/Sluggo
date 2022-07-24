# Dockerfile for sluggo app
# code lifted from: https://docs.docker.com/samples/django/

# build frontend stuff
FROM node:16.16.0 as ui-step
WORKDIR /ui
COPY ./Sluggo-SPA /ui/
RUN yarn && yarn build

# build backend stuff
FROM python:3
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# put all the code in the /app directory in the image
WORKDIR /app
COPY ./Sluggo-API /app/
RUN pip install -r requirements.txt

# copy the frontend files to the static dir
COPY --from=ui-step /ui/dist /app/api/static

CMD python3 ./manage.py runserver 0.0.0.0:8000
