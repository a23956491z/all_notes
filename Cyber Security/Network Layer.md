Two key of network layer function:

Data Plane: determine how datagram arriving router input and forward to output
Control Plane: determine how datagram routed among routers.
 * Traditional routing alg.
 * Software-defined networking (in remote server)

## Rouunter
Router architecture
![](https://i.imgur.com/V7u51Gs.png)

input port:
![](https://i.imgur.com/9px8Guj.png)
Queue: datagram arrive faster than forwarding rate.
Lookup: header fileld values lookup by forwarding table

### Forwarding
