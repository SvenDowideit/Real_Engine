FROM realengine/frontend:build as frontend

FROM python:3.6

COPY --from=frontend /frontend /frontend

WORKDIR /backend

# as we're containerized, we probably don't need a virtual env?
#RUN python -m venv venv
#RUN . venv/bin/activate ....

COPY . /backend
RUN pip install -e .

RUN mkdir instance
RUN python init_db.py

CMD ["python", "run.py"]
