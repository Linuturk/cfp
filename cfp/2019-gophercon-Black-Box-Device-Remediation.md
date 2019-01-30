# Black Box Device Remediation

## Format

* Keynote style presentations; 25 minute time limit, no questions from the floor.
* **Tutorial style presentations; 45 minute time limit, three tracks, questions at the presenter’s discretion.**

## Audience Level

* **All**
* Beginner
* Intermediate
* Advanced

## Elevator Pitch

At Netflix we test a wide variety of consumer electronics. These devices usually don't provide direct control points for automation. I'll be presenting on our software and hardware solution to black box device remediation.

## Description

We test a wide variety of consumer electronic devices that don't allow for direct control. We use a variety of external controls to detect a device's state and attempt automatic remediation. Learn how we migrated from a synchronous Flask API to an asynchronous Go API for device remediation in our labs. Our API make use of the [jsonapi.org](https://jsonapi.org/) specification to provide a consistent experience to our test runners. We utilize IOT devices and MQTT to send and process commands against our devices.

## Reviewer Notes

This topic has a solid migration story from a legacy Python API to a newly designed Go API. I'll be covering the limitations we faced due to the initial design of the first API, and how we designed the new API to solve for these problems:

* limited to a single AWS region
* new device models required code changes
* synchronous, blocking API calls up to 5 minutes long
* improper REST methods, ie GET that mutates state

We'll cover some of the problems we face in testing consumer electronics in a large automation lab:

* can't reliably detect state
* little to no consistency in direct access
* tests can leave devices in inconsistent states
* can't just pull the plug on some devices

I'll talk about our approach to management using external levers:

* infrared receivers
* physical and capacitive power buttons
* remote PDU access with on/off/measure features

The solution includes:

* using the [jsonapi.org](https://jsonapi.org/) specification and [api2go](https://github.com/manyminds/api2go) package.
* migrating from a Raspberry Pi hubs to a custom IOT device controlled using MQTT and the [paho.mqtt.golang](https://github.com/eclipse/paho.mqtt.golang) package.
* designing a custom command specification for the MQTT payloads to enable the control of IR transmitters and mechanical servo "fingers" for remote device manipulation. There are sections of the command specification package that have some inelegant marshaling solutions that I'd like to share with the community.
* using the [telnet]("github.com/ziutek/telnet) package to enable communication to our networked PDUs for power measurement and switching.
* reflection on structs to auto create our database schema.

I'd love some guidance on Audience Level and Format. I feel like a lot of this is fairly simple, but I've been immersed in this project for a while and I might not have a solid perspective on complexity. I'm sure there's plenty of content here to last 45 minutes, but a paired down presentation could fit in the 25 minute slot.

## Tags

go,golang,json,api,mqtt,iot

## Brainstorming

* Device remediation API rewrite from v1 (python) to v2 (go)
  * good migration story
  * more complete narrative versus a generic api / data store story
  * describe the problem we face testing consumer electronics
    * reliably detecting state
    * little to no consistency in direct access
    * tests can leave devices in inconsistent states
    * can't just pull the plug on every device
  * what levers do we have to pull?
    * infrared receivers
    * physical and capacitive power buttons
    * remote PDU access with on/off/measure features
  * v1 design limitations
    * limited to a single AWS region
    * new device models required code changes
* jsonapi.org spec API with api2go and Cassandra
  * not as interesting of a narrative but same technical aspects
* Windows service using go and github.com/kardianos/service
  * Windows is niche, which could be a pro or a con
* JSON Command spec for MQTT payloads
  * interesting IOT narrative
  * payload limitations make for creative engineering
  * never found an elegant solution for command validation and execution