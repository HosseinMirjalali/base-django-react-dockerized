FROM python:3.7.6-alpine3.11
LABEL maintainer="Hossein Mirjalali"

ENV PYTHONUNBUFFERED 1
# Installig python requirements 
COPY ./backend/requirements.txt /requirements.txt
RUN apk add --update --no-cache postgresql-client jpeg-dev
RUN apk add --update --no-cache --virtual .tmp-build-deps \
        gcc libc-dev python-dev musl-dev linux-headers postgresql-dev musl-dev zlib zlib-dev
RUN pip install -r /requirements.txt
RUN apk del .tmp-build-deps

# Creating and copying files to work directory.
RUN mkdir /backend
WORKDIR /backend
COPY ./backend /backend

# Creating seperate directories for Media and Static files. Also adding the user that Docker works with.
RUN mkdir -p /vol/web/media
RUN mkdir -p /vol/web/static
RUN adduser -D user
RUN chown -R user:user /vol/
RUN chmod -R 755 /vol/web 
USER user
