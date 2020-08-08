# node-express-monitoring

This PoC looks at how Metrics of a Node application can be obtained using least code possible.
This can be obtained using [appmetrics](https://github.com/RuntimeTools/appmetrics)
In this PoC we use:

* [appmetrics-dash](https://www.npmjs.com/package/appmetrics-dash): The appmetrics dashboard (path: <host>/appmetrics-dash) provides a live dashboard indicating various metrics of the application: memory,CPU HTTP Requests etc....
 
 ![alt text](/AppMetrics.png)
 
 
* [appmetrics-prometheus](https://www.npmjs.com/package/appmetrics-prometheus): Provides an endpoint (path: <host>/metrics) giving the metrics of the application in prometheus style output



