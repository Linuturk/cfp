# Title

## Format

* Keynote style presentations; 25 minute time limit, no questions from the floor.
* Tutorial style presentations; 45 minute time limit, three tracks, questions at the presenter’s discretion.

## Audience Level

* All
* Beginner
* Intermediate
* Advanced

## Elevator Pitch

You have 300 characters to sell your talk. This is known as the "elevator pitch". Make it as exciting and enticing as possible.

## Description

You should make the description of your talk as compelling and exciting as possible. Remember, you're selling both the organizers of the events to select your talk, as well as trying to convince attendees your talk is the one they should see.

## Reviewer Notes

Notes will only be seen by reviewers during the CFP process. This is where you should explain things such as technical requirements, why you're the best person to speak on this subject, etc...

## Tags

go,golang

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