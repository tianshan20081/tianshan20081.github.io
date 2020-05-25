---
title: 快速发布DockerCompose
date: 2020-05-25 10:16:23
tags: [Docker, Docker-compose, Flask]
---

### 基本信息

```
 # docker --version
Docker version 19.03.8, build afacb8b
 # docker-compose --version
docker-compose version 1.25.5, build 8a1c60f6
```

### 创建工程

```
 # tree
.
├── docker-compose.yml
└── product
    ├── Dockerfile
    ├── api.py
    └── requirements.txt
```

**product/api.py**

```py
from flask import Flask
from flask_restful import Resource, Api

app = Flask(__name__)
api = Api(app)

class Product(Resource):
    def get(self):
        return {'product': [ "Java", "Elixir","Flutter"]}

api.add_resource(Product, "/")

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

**product/requirements.txt**

```txt
Flask==0.12.0
flask-restful==0.3.5
```

**Dockerfile**

```Dockerfile
FROM python:3-onbuild
COPY . /usr/src/app
CMD ["python","api.py"]
```

**docker-compose.yml**

```yml
version: '3.6'

services:
  product-service-py:
    build: ./product
    volumes:
      - ./product:/usr/src/app
    ports:
      - 5001:80
```

### 启动服务

```
# docker-compose -f docker-compose.yml up
Starting docker-flask_product-service-py_1 ... done
Attaching to docker-flask_product-service-py_1
product-service-py_1  |  * Running on http://0.0.0.0:80/ (Press CTRL+C to quit)
product-service-py_1  | 172.18.0.1 - - [25/May/2020 02:26:37] "GET / HTTP/1.1" 200 -
```

访问服务 http://localhost:5001

```json
{ "product": ["Java", "Elixir", "Flutter"] }
```
