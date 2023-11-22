# Sandbox testing setup

**This guide will show you how to connect Twisto backend with Marqeta private sandbox enviorment and test transactions.**

# Setup

First replace `CARD_PRODUCT_TOKEN` in `twisto/apps/card/providers/marqeta.py`:

```
CARD_PRODUCT_TOKEN = 'b2775b04-8b6c-44ee-a2ef-23f5866a5aa8'
```

The sandbox is only reachable from our VPN - you have to add a route to the sandbox in the configuration.

For Mac:

```
sudo route -n add twisto-dev.marqeta.com -interface utun3
```

Where `utun3` interface is the interface your VPN is using - it may differ from machine to machine depending on your setup
You can list all interfaces with `ifconfig`, look for the one with ip address of our VPN (10.30.101.35), but it might change

# Webhooks

Webhooks are an essential part of the Marqeta platform. In order to consume them we need to expose the local server to the internet somehow.
[Serveo](http://serveo.net/) will take care of this. Simply run:

```
ssh -R 80:localhost:1234 serveo.net
```

and Servero will redirect
all trafic from https://\*something\*.serveo.net:80 to port 1234 on the local machine. You will see your public URL in the console.

Tell Marqeta about our new webhook endpoint (don't forgot to change the Serveo URL in json payload):

```
curl -X PUT \
  https://twisto-dev.marqeta.com/v3/fundingsources/programgateway/test_gateway_1/ \
  -H 'Authorization: Basic dHdzdF9zYW5kYm94X2FwaV9jb25zdW1lcjo1YzU4OTNjYi1hNDZiLTQ1YzUtOTg4MC04NTg5MGIwNzU0M2U=' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://*something*.serveo.net/marqeta/_/jit/"
}'
```

The last step is to run:

```
python client/marqeta.py/sandbox_proxy.py --listen_port 1234 --target_port 8000 --target_host api.cz.twisto.top:8000
```

This command will start a proxy server which stands between Serveo and the local Django app. It patches the Host header so the Django app is able to properly route the reqests and json payload of the messages to add `fraud` object which is normaly not present in sandbox enviorment. You can change the `target_host` to test transactions on different sites (e.g. `--target_host api.pl.twisto.top:8000`).

# Simulating

Let's export some variables:

```
export MARQETA_API_BASE_URL="https://twisto-dev.marqeta.com/v3/" \
MARQETA_API_USERNAME="twst_sandbox_api_consumer" \
MARQETA_API_PASSWORD="5c5893cb-a46b-45c5-9880-85890b07543e"
```

Now create a test user, spin-up Celery worker and a dev server on port 8000 then you can finaly begin [simulating transactions](https://www.marqeta.com/api/docs/WibxhCgAAGQ7I7-Y/simulating-transactions). Don't forget to export the valiables every time you open a new console window.

Example of an authorization transaction simulation with a webhook:

```
curl -X POST \
  https://twisto-dev.marqeta.com/v3/simulate/authorization \
  -H 'Authorization: Basic dHdzdF9zYW5kYm94X2FwaV9jb25zdW1lcjo1YzU4OTNjYi1hNDZiLTQ1YzUtOTg4MC04NTg5MGIwNzU0M2U=' \
  -H 'Content-Type: application/json' \
  -d '{
	"card_token": "6d084c2f-bb4a-43bb-b803-3ead91f126e0",
	"amount": 111,
	"mid": 111111,
	"webhook": {
    	"endpoint": "https://*something*.serveo.net/marqeta/_/webhook/",
    	"username": "my_username",
    	"password": "My_passw0rd"
	}
}'
```
