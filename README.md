# pa2
Programming Assignment 2

1. Why do you see a difference in webpage fetch times with small and large router buffers?

q20 fetch times:
Mean: 0.561128205128
Standard Deviation: 0.23250819445

q100 fetch times:
Mean: 1.10648484848
Standard deviation: 0.535414997425

Since h1 has a faster connection to the router than the uplink connection, the router buffer becomes a bottleneck to the connection.

When the buffer is full, it needs to be drained before TCP Congestion Control can resume. Hence, a larger buffer results in longer queues and higher latency delays since the packets take longer to drain. This consequently results in longer webpage fetch times.

2. Bufferbloat can occur in other places such as your network interface card (NIC). Check the output of ifconfig eth0 on your VirtualBox VM. What is the (maximum) transmit queue length on the network interface reported by ifconfig? For this queue size and a draining rate of 100 Mbps, what is the maximum time a packet might wait in the queue before it leaves the NIC?

Transmit queue length(packet), txqueuelen=1000 and Units per packet, MTU=1500.
Max time a packet waits = (1000 packets x 1500 bytes x 8 bits)/(100Mbps) = 0.12s

3. How does the RTT reported by ping vary with the queue size? Write a symbolic equation to describe the relation between the two (ignore computation overheads in ping that might affect the final result).

RTT = Queue_Size * Latency

RTT reported by ping is directly proportional to the queue size.

4. Identify and describe two ways to mitigate the bufferbloat problem.

Method 1: Implement QoS guarantees such as Traffic policing which limits the output rate.

Method 2: Employ Active Queue Management (AQM) algorithms which can indicate to the source networks that the buffer is filling up and to slow down the rate of transmission before buffer space is exhausted completely.