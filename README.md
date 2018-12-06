Portefølje 2 LEO1

The project has been executed as described in the instructions

Two containers has been created, one for serving a server to the outside and another to serve a randomness script to the first container.

The second container has an executable script ´rng.sh´ in ´/bin/rng.sh´. The program ´socat´ is used to serve the script on tcp port 8080. The command is ´socat tcp-listen:8080,fork,reuseaddr exec:/bin/rng.sh´

The first container has a lighttpd server. When requested, the server calls the second container's randomness script to retrieve some random numbers and replies to the client with a very simple HTML page.

In order for clients outside the raspberry pi to connect with the first container's webserver, iptables must be set up on the raspberry pi, forwarding the request. The following command forwards any tcp port 80 requests from the usb ethernet gadget connection to the ip adress of the container. (This example, the conatiner has IP 10.0.3.60)
´iptables -t nat -A PREROUTING -t usb0 -p tcp --dport 80 -j DNAT --to-destination 10.0.3.60:80´
