# Inter-Domain-Traffic-Engineering-and-MPLS-LSPs

RSVP-TE offers rich feature set for traffic engineering in MPLS backbone networks but RSVP-TE is dependent on IGP (ISIS/OSPF) for distribution of link state information across MPLS backbone networks which are usually designed to have single area (backbone area) stretched across whole MPLS BB. Having single IGP area stretched across whole MPLS BB network is simpler in term of configuration and troubleshooting / operation management but there is downside as well. Let's suppose MPLS backbone network scales to large extent and IGP is working stable but suddenly a situation happens where multiple links start flapping and as per IGP operation IGP link state advertisement will be re-flooded on each link flap across whole backbone network. Due to high resources in modern routers it should not pose any threat to stability of network but it's not only IGP link flaps that we need to worry about , but RSVP-TE itself also feed IGP (adjustable via configuration) about actual link bandwidth utilization and that information needs to delivered to whole MPLS backbone domain so that ingress PE routers can take decision for auto band witdh adjustment while keeping in view current bandwidth utilization of provider links. This information has to be distributed very fast across IGP / MPLS BB network and if it couples with extensive link flaps events then some awful situation could happen across MPLS BB (software stack could get into resource contentions to handle both of these events at same time)

To resolve above mentioned challenges , one approach could be to distribute IGP into multiple areas but problem is traffic engineering database (TED) which is populated from IGP traffic engineering information can not be traversed IGP boundaries. Hence RSVP-TE LSPs are dependent upon TED and due to non-availability of TED across multiple IGP areas RSVP-TE LSPs across multiple IGP areas would not come up.  Thanks to brilliant minds who contributed for [rfc7752](https://datatracker.ietf.org/doc/html/rfc7752) , this RFC explains operation of BGP-LS (link stat) where IGP link state information from TED can be distributed via BGP.

