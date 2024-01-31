---
layout: page
title: Measurement traffic
---

If you are encountering problems with our anycast measurements, please read on to learn what to expect from us, how to reach out to us, and, as a last resort, how to block our traffic.
We thank you in advance for working with us to resolve any issues, and apologize in advance if we have inadvertently caused problems through our measurement.

### What traffic to expect?

Our measurements consist of a series of TCP, UDP, or ICMP packets sent to at most one IP address per /24 prefix. All packets are spaced at least 1 second apart. The order in which prefixes are selected is random to minimize load to larger networks.
Our traffic originates from the following IP ranges: `145.100.118.0/23` and `2001:610:9000::/40`.

### What to do if our measurements cause inconvenience?

We are committed to responsible network measurement practices to minimize the impact on infrastructure. If you believe our traffic is negatively affecting your systems, please [contact us](/contact) so that we can work to resolve the problem. When reaching out to us, please provide the following information:

1. Your organization's name and a point of contact (name and email adddress).
2. The IP address(es) or prefixes from which you are receiving problematic traffic.
3. A description of the impact, including details such as the number of queries per second and their effects.
4. The date and time when you first observed problems that may be related to our measurements.

### Blocking our traffic

If you determine that it is necessary to block our traffic, we kindly request that you notify us so we can still exclude you from our measurements.
