# panda-analytics
In-House Web Analytics Made Easy

# Description
This is a place-holder for the moment, but I'm pretty sure a simple prototype could be knocked out in a day or so.  I had an idea that there should be a good solution for people that want to use Web analytics to improve their site and monitor traffic, but they don't want to ship all their user's data to Google or their competitors.  This is an open-source, in-house solution.  The need to deploy Elasticsearch and Kibana with your site (even a static content site) would make this technology a great example deployment for Huxley.  :)

Open sourced Node library that you drop into your server.  In the actual server code, all you'd have to do is feed it your request:
```coffee
http = require "http"
panda_analytics = require "panda-analytics"
{async} = require "fairmont"

analytics = new panda_analytics
analytics.es_target = "http://es.[user-domain].com:9220"

server = async (request, response) ->
  yield analytics.input request
  response.writeHead 200
  response.write "Hello World!"
  response.end()

http.createServer(server).listen(80)
```

Panda-Analytics would parse the HTTP request for relevant data and dump it all into an Elasticsearch cluster.  Kibana would be there to provide visualizations like the ones you see in Google Analytics.
