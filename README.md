# ProxyAgent

This is a module which simply provides an HTTP(S) `Agent` which allows for requests/connections to be made through an
HTTP(S) proxy.

## Usage

### ProxyAgent.getAgent(secure[, proxyUrl[, proxyTimeout]])
   - `secure` - `true` if this agent will be used for secure (HTTPS) requests, or `false` if not
   - `proxyUrl` - The URL to your proxy, or something falsy to just get `false` returned (indicating no agent)
   - `proxyTimeout` - The timeout for connecting to the proxy in milliseconds; default `5000` (5 seconds)

```js
const ProxyAgent = require('@doctormckay/proxy-agent');
const HTTPS = require('https');

HTTPS.get({
    "host": "icanhazip.com",
    "port": 443,
    "agent": ProxyAgent.getAgent(true, "http://user:pass@1.2.3.4:12345", 10000)
}, (res) => {
	if (res.statusCode != 200) {
		console.log("HTTP error: " + res.statusCode);
	}
	
	res.on('data', (chunk) => {
		console.log(chunk.toString('utf8'));
	});
}).on('error', (err) => {
	console.log(err);
});
```
