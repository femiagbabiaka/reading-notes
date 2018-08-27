# Introduction

* `TCP/IP` is a protocol suite that implements the Internet architecture and draws its origins from the _ARPANET Reference Model_.
  * The ARM was influenced by early work on packet switching in the United States by Paul Baran and Leonard Kleinrock.
* `TCP/IP` evolved from work that addressed a need to provide interconnection of multiple different packet-switched computer networks.
  * This was accomplished using a set of `gateways` (routers) that provide a translation between each interconnected network.
  * The resulting concatenated network (inter-network) is more useful because of the number of different services that can be connected.

## Architectural Principles
* There were several goals underpinning the creation of the Internet architecture.
  * Primary Goal
    * To develop an effective technique for multiplexed connection of existing interconnected networks.
  * Secondary Goals
    * Internet connection must continue despite loss of networks or gateways.
    * The Internet must support multiple types of communication services.
    * The Internet architecture must accomodate a variety of networks.
    * The Internet architecture must permit distributed management of its resources.
    * The Internet architecture must be cost-effective.
    * The Internet architecture must permit host attachement with a low level of effort.
    * The resources used in the Internet architecture must be accountable.

### Packets, Connections, and Datagrams
* One of the important concepts developed in the 1960's was the idea of `packet switching`.
  * In packet switching, chunks of digital information comprising some number of bytes are carried throughout the network somewhat independently.
  * Chunks coming from different sources or senders can be mixed together and pulled apart later, which is called `multiplexing`.
    * This has two advantages:
      * The network can be more resilient.
      * here can be better utilization of the network links and switches.
  * When packets are received at a packet switch, they are ordinarily stored in buffer memory or queue and processed in a FIFO fashion.
  * Virtual circuits that exhibit many of the behaviors of circuites but do not depend on physical circuit switches can be implemented on top of connection-oriented packets.
    * The book does quite a bad job at describing connection oriented networks, but here is a basic synopsis:
      * VC abstraction and connection oriented packet networks such as X.25 require state to be stored in each switch for each connection.
      * This is because each packet would only carry a small bit of overhead information that provides an index into a state table. At each switch, the identifier contained in that overhead information is used in conjuction with the per-flow state in each switch to determine which switch the packet should be passed along to next.
      * The per-flow state is established prior to the exchange of data using a signaling protocol that supports connection establishment, clearing, and statu information.
  * Connection-oriented networks were the most prevalent form of networking for many years. In the late 1960's, another option was developed known as the datagram.
    * A datagram is a special type of packet in which all of the identifying information of the source and final destination resides in the packet itself, instead of in those lookup tables stored in each switch.
  * Datagrams enabled what we call a `connectionless network`.

### The End-To-End Argument and Fate Sharing
* An important principle that influence the design of the TCP/IP suite is called the `end-to-end argument`.
  * This priciple basically states that features needed by consumers of a protocol should be implemented by the consumers, and not by the protocol itself. 
  * Efforts to correctly implement what the application is likely to need are doomed to incompleteness.
  * In TCP's case, being designed with the end-to-end argument in mind means that it supports a design with a "dumb" network and "smart" systems connected to the network.
* Another important principle is that of `fate sharing`.
  * This basically means that all of the state necessary to maintain an active connection should live at the ends of that connection.
  * Because of this, the only failure that could take down a connection is when one of the endpoints fail, in which case, the connection should die anyways.

