# Product aggregator microservice
  
REST API JSON Python microservice, which allows to browse a product catalog and
automatically updates prices from the external offer service (provided by Applifting).

## Main Features:
- API allowing to create, update and delete product
- Periodically query provided microservice for offers/shops with products - currently set for 600 seconds

## API Endpoints:

All responses have the form of JSON.

** request **

'GET /product/{name}'

** headers **

None

** response **

200 on success
```
{
    "product_id": 1010,
    "name": "fotak",
    "description": "nejlepsi fotak"
}
```
404 if not found
```
{
    "msg": "product 'mycka' not found"
}
```

** request ** 

'POST /product/{name}'

** headers **
```
{
    "description": {string}
}
```
** response ** 
 
201 created
```
{
    "msg": "product 'televize' created & registered with id: 1012"
}
```
400 bad request
```
{
    "msg": "product 'televize' already exists"
}
```

** request **

'DELETE /product/{name}'

** headers ** 

None

** response **

200 on success
```
{
    "msg": "product 'televize' deleted"
}
```
404 not found
```
{
    "msg": "product 'sekacka' not found"
}
```
** request **

'PUT /product/{kamera}'

** headers ** 
```
{
    "description" : {string}
}
```

** response **

201 on success (creation)

```
{
    "msg": "product 'kamera' created & registered with id: 1013"
}
```
200 on success (update)
```
{
    "msg": "product 'kamera' updated"
}
```

** request **

'GET /products'

** header ** 

None

** response **

200 on success
```
{
    "products": [
        {
            "product_id": 1010,
            "name": "fotak",
            "description": "nejlepsi fotak"
        },
        {
            "product_id": 1011,
            "name": "iphone",
            "description": "nejlepsi iphone"
        }
    ]
}
```

** request **

'POST /offer/{int}'

** headers ** 

None

** response ** 

200 success

(returns list of all offers for a product registered under particular id on the external offers API)

404 not found

(returns empty list)

** request **

'GET /offers'

** headers ** 

None

** response 

200 success

(returns list of all offers from local database)

## Instalation

Installation via requirements.txt:

```
- git clone https://github.com/ExperimentalHypothesis/flask-applifting-api-ms.git
- cd flask-applifting-api-ms
- python3.7 -m venv venv
- source venv/bin/activate
- pip install -r requirements.txt
```

## Run
To run it type:
```
python wsgi.py
```








