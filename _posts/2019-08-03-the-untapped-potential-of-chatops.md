---
title: "The Untapped Potential of ChatOps"
published: true
---

# ChatOps

Six months ago, I was introduced to the concept of `ChatOps`. Yes, I know a little late. Mind you, I was still new to the "Infrastructure as a code" world but I was immediately intrigued by its simplicity, ease of implementation and its impact on day to day operations. ChatOps is a what it sounds like, day-to-day operations, simplified to through chat. In this case we used Slack combined with our Cloud provider: IBM Cloud (AKA SoftLayer).  

In came, `gobot` (Yes, it's written in Go, we're lazy and undecisive people when it comes to names). Our very own, personalized solution for our day to operations in dealing with infrastructure. It's still in its alpha stages but we've seen an immediate change in:

## Response Times
One of the first features we implemented was an ability to control power over our infrastructure. Often times we run into issues where a simple reboot is required. We simplified this to:

```bash
gobot <poweroff|poweron|reboot> <hostname|ip>
```

and of course the little bit of code it runs. Simple, straightforward, and ridiculously easy to implement on your backend.

```bash
slcli vs power-off <ID>
```

## Alert Fatigue
One of the other "quirks" we noticed on a daily basis was:

- Person A: Hey is anyone working on cluster `abcdefg`?
- Person B: Yes John, I am.
- Person A: Well, then tell me so I don't get alerted you douche. 
- Person B: My bad. *runsaway*

The simple solution: alert supression. We defined a set of "maintenance windows". 

```bash
gobot maintenance <product>
```

This would then pop up options for a `clustername`, `duration` and optional `datacenter` option. You can supress alerts for particular clusters, particular data centers or supress all alerts in case of a worldwide maintenance window **for a period of time**. 

## Information 
The last and maybe the most used feature we implemented was the ability to look up device information. A simple

```bash
gobot lookup <hostname|ip>
```

This returned information such as:
- Hostname
- Private IP
- Public IP
- Account Number
- Environment (Prod/Non-Prod)
- Data Center
- Tags
- VLAN
- Subnet(s)
- Type of Instance (Hardware, VSI)
- OS
- POD

...etc

This vastly simplified having to login with our cloud provider, lookup devices and fetch any/all information from 5 different places. 

## Quirks

One of the things we found challenging in this endeavour:
- Authentication: The more features we implement, the more we realize Slack allows anyone to install the App to any workspace within the organization and we definitely don't want other people having the ability to mess with our infrastructure. 
- Timezones: Slack doesn't like timezones apparently. It's oddly challenging to read user input as time. Don't believe me? Try it! 

New things don't come without their quirks but we're definitely up for the challenge. I invision a future where almost all day-to-day operations are handled through chat. Bold, but the more we tackle issues, the more it feels like a reality. 
