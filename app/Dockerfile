FROM python:3.9-slim

WORKDIR /app

RUN apt-get update 

COPY . /app

RUN pip3 install -r requirements.txt

EXPOSE 8000


ENTRYPOINT ["streamlit", "run", "main.py", "--server.port=8000", "--server.address=0.0.0.0"]`
