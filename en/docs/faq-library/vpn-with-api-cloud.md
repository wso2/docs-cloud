# VPN Connection with API Cloud


1.  #### **How much bandwidth is guaranteed?**

    We do not have any bandwidth limitation on our end. There is a
    defined idle period. If the connection is idle for more than the
    given period it will be closed. The connection will be reestablished
    at the next immediate call, when it is active again.

2.  #### **Would DNS resolution in API Cloud be done inside our network or using your own DNS service?**

    This will be done in our DNS service. However, you need to map the
    CNAME entry on your end as well. **  
    **

3.  #### **Does your VPN solution have high availability? Do you have replicated VPN nodes?** 

    We do not have replicated VPN nodes on our end instead we use the
    method of having replicated VPN endpoints for automatic fail over
    which routes to the other endpoint in case one endpoint fails and
    guarantees high availability. **  
    **
