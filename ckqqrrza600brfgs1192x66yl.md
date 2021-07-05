## HTTP/2 With (Ruby/Sinatra + Puma) + Nginx server

Notes on how to enable HTTP/2 on Puma via `early_hints`, and enabling HTTP/2 on a reverse-proxy nginx server.

*(Or any other rack-based gem, like Rails)*

In time, the [Puma Rack-based server](https://puma.io/) gained HTTP/2 capabilities, but you need to enable it.

Given that one starts Puma with something like `puma -C config/puma-config.rb`, let's add one line of code into it:

`early_hints true`

Add that anywhere in **"puma-config.rb"**, and Puma now has *HTTP/2* capabilities.

With the Ruby server taken care of, I'm assuming you are also using nginx as a reverse proxy for Puma (possible upcoming notes), and that https (ssl) is properly setup (more notes).

In `/etc/nginx/nginx.conf` or the respective place that contains the configuration for the nginx file for your install, we change any listens on **port 443 (ssl)**, and possibly ** 80 **by adding http2 to the end of it (I have not tested it with port 80, as my website is https only):

ex:

`listen 80;` -> `listen 80 http2`

`listen [ :: ]:80` -> `listen [ :: ]:80 http2`

so,

listen 443 ssl http2;

listen [::]:443 ssl http2; 

Then a `service nginx restart` and your nginx server is now running on HTTP/2!

With these two options enabled in Nginx & Puma, you now have a server running in HTTP/2.

Ways to check: A HTTP version indicator addon for either Firefox or Chrome.

On Firefox:  [HTTP Version Indicator](https://addons.mozilla.org/en-US/firefox/addon/http2-indicator/) 