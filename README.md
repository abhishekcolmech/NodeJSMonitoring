# Application and Platform Monitoring:

Please follow below steps to deploy NodeJSMonitoring source code inside a Docker Container.

    1. Clone the repo with master branch and go inside the directory,

    2. Run below command in order to build docker image out of Dockerfile. It will compile the source code and build Node.js application inside the docker image.

        **  docker build -t node-express-monitoring . **
    
    3. Run below command to spwan a Container out of an image we just built,
        
        ** docker run -p 3000:3000 --name sample_node_container -d node-express-monitoring **
    
    4. Now we can access the Node.js application we just built in a Container. Hit below urls from your browser to view UI and other monitoring stats.

**URLs:**

 **App UI:** http://<host-ip>:3000

 **Appmetrics Dashboard:** http://<host-ip>:3000/appmetrics-dash/

 **Prometheus Metrics:** http://<host-ip>:3000/metrics


### Application Monitoring:

Here we are monitoring the deployed Node.js app through Appmetrics-dash.

 Appmetrics-dash enables us to see the performance of our Node.js application via a dashboard. The dashboard use Node Application metrics to monitor the application.

 This can be obtained using [appmetrics](https://github.com/RuntimeTools/appmetrics)

Here, we use:

* [appmetrics-dash](https://www.npmjs.com/package/appmetrics-dash): The appmetrics dashboard (path: <host>/appmetrics-dash) provides a live dashboard indicating various metrics of the application: memory,CPU HTTP Requests etc....

 ![alt text](/images/AppMetrics.png)


* [appmetrics-prometheus](https://www.npmjs.com/package/appmetrics-prometheus): Provides an endpoint (path: <host>/metrics) giving the metrics of the application in prometheus style output


    Details of setting up the Node Application Metrics Dashboard can be found here:https://www.npmjs.com/package/appmetrics-dash

### Container Health-Check Monitoring:

    1. In order to check the health of a Container, we have added HEALTHCHECK instructions in Dockerfile.
    The HEALTHCHECK instruction can be specified as:

        HEALTHCHECK <options> CMD <command>

        The <options> can be:

            --interval=DURATION (default 30s).

            --timeout=DURATION (default 30s).
    
    2. The <command> is the command that runs inside the container to check the health.

        If health check is enabled, then the container can have three states:

               ** Starting:** Initial status when the container is still starting.

               ** Healthy:** If the command succeeds, then the container is healthy.

               ** Unhealthy:** If a single run of the <command> takes longer than the specified timeout, then it is considered unhealthy. If a health check fails, then the <command> will run retries number of times and will be declared unhealthy if the <command> still fails.

        The commands exit status indicates the health status of the container. The following values are allowed:

        **0**: container is healthy.

       **1**: container is not healthy.

    3. We can see the container health is like below. As it shows STATUS "healthy"

![alt text](/images/docker_ps.png)


    4. We can also run below command to get the detailed view of Container health in JSON format.

        ** docker inspect --format='{{json .State.Health}}' sample_node_container **

    5. We can also get the Docker stats in JSON format by running below command.

        ** docker stats --no-stream --format "{{ json . }}" sample_node_container **
    
![alt text](/images/docker_stats1.png)

![alt text](/images/docker_stats2.png)

    6. Taking the output of above json, we can then make any short of alert mechanism to report about the container health.
