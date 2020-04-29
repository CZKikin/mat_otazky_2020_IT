# 15. Směrování a směrovací protokoly

## RIPv2
Routing Information Protocol version 2 (RIPv2), was a common LAN routing protocol in the '90s, 
but is rapidly fading away in production networks. RIPv2 suffered from scalability issues due to 
a relatively low maximum hop count of 15 routing devices. 
Compared to more modern dynamic routing protocols, RIPv2's methods for selecting optimal 
¨routes and the substantial convergence time it takes to recalculate paths renders it nearly obsolete. 
Today, the only reason you might run across a network running RIPv2 is either that the 
network is very old and in serious need of an upgrade or the network 
is running cheaper, consumer-grade routing hardware that can only support RIP.