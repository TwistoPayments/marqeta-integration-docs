# Card details

Because we are not [PCI compliant](https://www.investopedia.com/terms/p/pci-compliance.asp) and we cannot get card numbers, we have to use a [Marqeta iframe and Javascript](https://www.marqeta.com/docs/developer-guides/using-marqeta-js#_tutorial) for displaying the details.

## Implementation

To get the details, we need to get a control token (`marqeta.ApiProvider.get_client_token`) and pass it to MQ javascript.

### Web

Web is using CreateCardWidget mutation and renders the iframe by itself

### Mobile

Marqeta iframe has a problem with being rendered from pure HTML in a mobile webview. That's because the JS is accessing `window.location.origin` which is null in such scenario.
Thats why a new view `CardDetailsView` had to be created so the mobile apps can open the webview with url and MQ JS won't be complaining.
This poses a security issue though, because the user doesn't have to be logged in in the webview and we can pass only URL query params there.
Solution for this is using one time links which will expire once the user opens it (`MarqetaCardDetailLink`)

## Testing

Marqeta mock (`app.ClientTokenView`) has client credentials for sandbox for the control token. IPs accessing the sandbox have to be whitelisted - our VPN is - so you need to route the traffic there from your local machine:

###### Mac

```bash
sudo route -n add `twisto-dev.marqeta.com` -interface utun3  # the `utun<X>` may differ on your machine, its your VPN interface
```

###### Liunx

```bash
sudo route add -host twisto-dev.marqeta.com dev tun0  # the `tun<X>` may differ on your machine, its your VPN interface
```

You can also use `marqeta-mock/iframe/` view to toy with the iframe. You can pass a production control token into `test_token` query param which you can get from GQL request on production.

You can also use the sandbox [directly](./guides/sandbox.md) instead of MQ mock (if you are lazy to run the mock), but you have to hardcode the existing card token on the sandbox when using it

**The details you will receive from the sandbox will be always the same and won't reflect the card details on a test server.**
