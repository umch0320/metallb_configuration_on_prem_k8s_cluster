# metallb_configuration_on_prem_k8s_cluster
Installation by Manifest

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.9/config/manifests/metallb-native.yaml

Defining The IPs To Assign To The Load Balancer Services
In order to assign an IP to the services, MetalLB must be instructed to do so via the IPAddressPool CR.

All the IPs allocated via IPAddressPools contribute to the pool of IPs that MetalLB uses to assign IPs to services.

![image](https://user-images.githubusercontent.com/107995013/236740614-75ef98bf-282f-4ef3-9c4a-aee7230c6b72.png)

  
  In order to advertise the IP coming from an IPAddressPool, an L2Advertisement instance must be associated to the IPAddressPool.

For example, the following configuration gives MetalLB control over IPs from 192.168.1.240 to 192.168.1.250, and configures Layer 2 mode:

![image](https://user-images.githubusercontent.com/107995013/236740324-6f8f06a3-ecb3-47e3-b28f-f96662d61ed3.png)

Setting no IPAddressPool selector in an L2Advertisement instance is interpreted as that instance being associated to all the IPAddressPools available.

So in case there are specialized IPAddressPools, and only some of them must be advertised via L2, the list of IPAddressPools we want to advertise the IPs from must be declared (alternative, a label selector can be used).

![image](https://user-images.githubusercontent.com/107995013/236740444-0ff52eea-6542-41ac-b9cc-a41574dc1dca.png)
