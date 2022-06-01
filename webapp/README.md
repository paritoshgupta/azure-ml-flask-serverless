- docker build --build-arg VERSION=AutoMl_123 -t flask-predict .
- docker images flask-predict
- docker run -p 5000:5000 -d --name flask-predict flask-predict
- curl 192.168.0.200:5000
- python predict.py # requests library to send a POST request and process a response back