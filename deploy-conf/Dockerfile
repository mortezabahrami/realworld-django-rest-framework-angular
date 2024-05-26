FROM python:3.12

ADD backend/requirements.txt /app/requirements.txt

WORKDIR /app
RUN pip install --upgrade pip setuptools wheel
RUN pip install -r requirements.txt

ENV VIRTUAL_ENV /env
ENV PATH /env/bin:$PATH
ENV PYTHONPATH /app
ENV C_FORCE_ROOT true
ENV DJANGO_SETTINGS_MODULE config.settings

CMD ["python", "manage.py", "makemigrations"]

EXPOSE 8000
ENTRYPOINT python manage.py migrate && gunicorn --bind 0.0.0.0:8000 --workers=2 config.wsgi
