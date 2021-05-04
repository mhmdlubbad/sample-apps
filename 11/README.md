# Celery Distributed Task Query with FastAPI for Machine Learning

This sample app demonstrates how to implement Celery distributed task queues on top of RabbitMQ broker for Machine Learning model training and data processing. We are using TensorFlow in this example to train the model. API request comes through FastAPI and it is being processed asynchronously by Celery. There is a separate API endpoint to check task status. Multiple requests can be initiated and processed at the same time in parallel. Celery tasks can be monitored using Flower monitoring tool.

* [Celery documentation](https://docs.celeryproject.org/en/stable/index.html)
* Machine Learning [model](https://towardsdatascience.com/multi-output-model-with-tensorflow-keras-functional-api-875dd89aa7c6) used in this app
* [Flower](https://flower.readthedocs.io/en/latest/) - Celery monitoring tool

## Commands (executed from celery-web folder)

* Start FastAPI endpoint
  * ** uvicorn endpoint:app --reload**
* Start Celery worker
  * ** celery -A boston_housing.worker worker --loglevel=INFO **
* Start Flower monitoring dashboard
  * ** celery flower -A boston_housing.worker --broker:pyamqp://guest@localhost **

API url: http://127.0.0.1:8000/api/v1/bostonhousing/docs
Flower url: http://localhost:5555/tasks