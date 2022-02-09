Now that we have our environment set up, our TG solution established, and our queries installed and ready to be utilized, let's set up our middleware!

## Connect to your TigerGraph Solution

Open `main.py` in your `middleware` directory and import pyTigerGraph and configs. configs is going to be out configuration file for our TG solution credentials.

```python
import pyTigerGraph as tg
import configs as Credential
```

Now create a new `configs.py` file in the middle folder and import the TG credentials you created your solution with as shown below.

```python
HOST='https://flutter-app.i.tgcloud.io'
USERNAME='tigergraph'
PASSWORD='password'
GRAPHNAME='productGraph'
```

Back in the `main.py` file, create a connection to your TG Cloud server using pyTigerGraph. 

```python
conn = tg.TigerGraphConnection(host=Credential.HOST, username=Credential.USERNAME, password=Credential.PASSWORD, graphname=Credential.GRAPHNAME)
conn.apiToken = conn.getToken(conn.createSecret())
```
*Check out the [pyTigerGraph documentation](https://pytigergraph.github.io/pyTigerGraph/GettingStarted/).*

Save the `main.py` and `configs.py` files, and if it runs and reloads successfully, then you are connected to TG Cloud!

## Establish Cross-Origin Resource Sharing (CORS)

Since a port is not specified, CORS configuration is essential.

Import CORSMiddleware in the `main.py` file.

```python
from fastapi.middleware.cors import CORSMiddleware
```

Create allowed origins (none in this case).

```python
origins = ["*"]
```

Specify what the middleware allows:

* Credentials
* HTTP methods
* HTTP headers

```python
app.add_middleware(
   CORSMiddleware,
   allow_origins=origins,
   allow_credentials=True,
   allow_methods=["*"],
   allow_headers=["*"],
)
```

## Create Query Endpoints


**IMPORTANT NOTE**: Don't forget that your TG solution should be started and running before API requests can be established through FastAPI and Flutter! Go to the [TigerGraph Cloud](tgcloud.md) page to set up your TG solution if you have not already done so. 