+++
title = "About lazy-jar"
date = ""
+++

Lazy-Jar is a slack app for scheduling remote stand-ups and tracking participation

Simply create a stand-up with the following example:

`/lj schedule myStandUp with @shaniqua and @batman everyday at 10 am UTC`

Once a stand-up is created, Lazy-Jar  will notify all stand-up members 5 minutes prior the start of every stand-up by sending them a link to a video chatroom. Lazy-Jar tracks member participation by keeping track of which of the links it had sent were clicked on. The link disappears after the end of a stand-up meeting.
<br>

## How does it work?

Every command goes through the following stages

1.  **Parsing**: the command is transformed into an action (JSON representation) that is easily consumed by the other modules in the system
2.  **Action Validation**: validates an action and transform its properties to create an action
3.  **Reducer**: given the current state for a team and a valid action, returns the next state


<br>

## Full Command Documentation

### Definitions

* `name` is a unique identifier for a stand-up
* `when` identifies when and how often an event should happen such as "everyday at 6:00 pm", or "every workday at 4:30 pm"
* `time range` identifies a period of time such as "1 week", or "3 days"
* `time zone` identifies the timezone corresponding to the `when` input

### Command Syntax

* #### Schedule a new stand-up with a group of hackers
    `/lj schedule [name] with [list of @hacker] [when] [time zone]`
  * e.g. "schedule artris with @dtoki and @alireza everyday at 6:00 am America/Vancouver"
  * When there is a conflict, the hacker will not be added to the new stand-up and a warning will be displayed
  * If a stand-up with the same name already exists, the user will get asked to provide a different name
  

* #### Add hackers to an existing stand-up
    `/lj add [me or list of @hacker] to [name]` 
  * e.g. "add @dtoki and @alireza to artris"
  * When there is a conflict, the hacker will not be added to the new stand-up and a warning will be displayed

* #### Remove hackers from an existing stand-up
    `/lj remove [me or a list of @hacker] from [name]`
  * e.g. "remove me from artris"
  * An error message will be displayed if the hacker does not belong to the specified stand-up

* #### Reschedule a stand-up
    `/lj move [name] to [when] [time zone]`
  * e.g. "move artris to everyday at 7:00 am America/Vancouver"
  * A warning will be displayed if the new schedule results in conflicts among participant hacker schedules

* #### Temporarily halt a stand-up
    `lj halt [name]`
  * e.g. "halt artris"

* #### resume a currently halted stand-up
    `lj resume [name]`
  * e.g. "resume artris"

* #### Terminate a stand-up
    `/lj terminate [name]`
  * e.g. "terminate artris"


* #### Notify an individual's timed break for a stand-up
    `/lj [I or @hacker] will skip [name] [time range]`

  * e.g. "I will skip artris for 2 weeks"
  * An error message will be displayed if the hacker is not part of the standup

* #### Stop notifying a hacker
    `/lj stop notifying [me or list of @hacker] for [name]`
  * The hacker is on a break and will not be counted as part of a stand-up until a corresponding 'start' command is sent
  * e.g. "stop notifying @grace for artris"
  * An error message will be displayed if the hacker is not part of the standup

* #### Start notifying a hacker 
    `/lj start notifying [me or list of@hacker] for [name]`
  * e.g. "start notifying @grace for artris"
  * An error message will be displayed if the hacker is not part of the standup

* #### Display info on all active stand-ups and member participation
    * `/lj status`

<br><br>

### FAQ

