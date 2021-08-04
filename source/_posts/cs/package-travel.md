---
title: 数据包传输过程
date: 2021-07-20 15:53:44
categories:
计算机
tags:
---

​        网络最终的目的是实现计算机之间的通讯，为了实现这个功能，一共需要7个模块相互协作，每一个模块都是独立可替换的，完成自己特定的任务，这个七个模块统称为OSI Model (Open System Interconnect)，字面意思，开放的不同系统之间可以通讯的协议

![image](https://www.practicalnetworking.net/wp-content/uploads/2016/01/packtrav-osi-layers-236x300.png)



### OSI Layer 1 – Physical

​    The Physical layer of the OSI model is responsible for the transfer of bits - the 1's and 0's which make up all computer code.

This layer represents the physical medium(of middle size) which is carrying the traffic between two nodes.An example would be your Enthernet cable or Serial Cable.But don't get too caught up on the word "Physical" - this layer was named in the 1970s,long before wireless communication in networking was a concept.As such,WiFi,despite it not having a physical, *tangible*(clear enough to be seen) presence,is also considered a Layer 1 protocol.

![image](https://www.practicalnetworking.net/wp-content/uploads/2016/01/packtrav-physical-wires-1024x221.png)

Aside from the physical cable,Repeaters and Hubs also operate at this layer.

![image](https://www.researchgate.net/profile/Digbijay-Guha/publication/319317581/figure/fig6/AS:532380131180544@1503940722129/Fig-6-Repeater-41-Types-of-Repeater-Telephone-Repeater-This-is-used-to-enhance-the.png)

A Repeater simply repeats a signal from one medium to the other,allowing a series of  cables to be daisy  chained together and increase the range a signal can travel beyond the single cable limit.These are commonly used in large WiFi deployments,where a single WiFi network is "repeated" throughout multiple access-points to cover a larger range.



A hub is simply a multi-port Repeater.If four devices are connected to a single Hub,anything sent by one device gets repeated to the other three.



参考：https://www.practicalnetworking.net/series/packet-traveling/packet-traveling/



https://www.practicalnetworking.net/series/packet-traveling/osi-model/

