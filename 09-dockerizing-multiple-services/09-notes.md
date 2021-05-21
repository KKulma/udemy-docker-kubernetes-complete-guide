### Nginx pah routing

We need a service that will receive requests from the website and decide whether to pass them onto the React Server or Ezpress Server, based on their path. This is the role that Nginx is going to play, e.g. if it contains `//api/` then it will pass it to Express otherwise to React.

To enable this communication, we could set ports for React Server and Express Server, but in this case we're going to rely on the path, as ports can easily change depending on the environment the containers are run in 


### Routing with Nginx 

`default.conf` - a very special fille ;) that adds configuration rules to Nginx, e.g.
- tells nginx that there us an upstream server at client:3000
- tells nginx that there is an upstream server at server:5000
which can be translated into: 

- Listen on port 80
- if anyone comes to '/' send them to client upstream
- if anyone comes to '/api' send them to server upstream,