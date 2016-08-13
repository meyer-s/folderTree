# Cisco Switch Configuration

Telos provides us with a basic switch configuration for the 2960G and 2960S switches. Essentially this does two things:

* Enable IGMP snooping on all ports, along with IGMP v2 "immediate leave" (which instructs the switch to immediately cease transmitting data the moment a node gives a leave notification)
* One switch in the network needs to be the IGMP querier. The default behavior is that only one querier will exist on the network at a time, usually through an election process which supposedly selects the lowest IP address. The IGMP querier is going to control all the streams, so it's important that it be the most central switch in the network. The tower switch should be configured as a backup querier (querying enabled but not elected, accomplished by telling the Control switch to be a master)

##QoS Config

QoS ought to be enabled. Basically Livewire audio is tagged with a Class-of-Service (CoS) tag (each tag can range from 0-7). The function of the QoS simply needs to ensure that Livewire data gets sent first and that the regular data will be dropped first in the event of a link saturation.

We can simply separate out livewire audio by its CoS tag, configured on the node page. By default, standard streams get CoS 5 and Live streams get CoS 6. The switch then sorts these into queues, usually 4 of them but it's configurable, and each queue gets a priority.

The 2960 series switches support Shared-Round-Robin or srr scheduling, whereas the SG500 series support weighted-round-robin or wrr scheduling. See the relevant ops list thread, but these are apparently almost the same except that srr is "better" in that it ends up sending traffic more evenly as opposed to wrr sending traffic more bursty.

###2960 vs 2960-S

The 2960-S is a stackable switch. It does not support ingress queueing, only egress. The 2960C 8 port switch supports both ingress and egress queueing.

The 2960 supports a single `priority-queue` which accomplishes the same thing as the `strict` setting on the SG500, however (confusingly) the `priority-queue` is applied to Queue 1 instead of starting at Queue 4 in the SG500. Packets entering into Queue 1 when enabled in priority-queue mode are then serviced before any other packet. The mapping is as follows:

```
CONS48#show mls qos maps cos-output-q
   Cos-outputq-threshold map:
              cos:  0   1   2   3   4   5   6   7
              ------------------------------------
  queue-threshold: 2-1 2-1 3-1 3-1 4-1 3-1 1-1 1-1
```

### SG500 Setup

Live Stream gets CoS 6 and goes into Queue 4. Queue 4 is given "strict" mode therefore its traffic will always be forwarded first.

Standard Stream gets CoS 5 and goes into Queue 3. We can then use strict or wrr to prioritize the data. Wrr and srr both function based on the ratio of the numbers. Usually you would use "shared" mode for each in which quotas are guaranteed but will provide maximum bandwidth available, whereas "shaped" would enforce the limit regardless of whether the channel was completely open.

The ports must be configured to trust the CoS tag on the incoming packets. (There are other ways to classify packets into queues, like by port or by DSCP tag.)
