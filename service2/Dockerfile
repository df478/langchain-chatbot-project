FROM python:3.10-slim-buster

WORKDIR /app

COPY ./service2/. /app

RUN pip install --no-cache-dir fastapi uvicorn redis requests openai

EXPOSE 80

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "80"]
