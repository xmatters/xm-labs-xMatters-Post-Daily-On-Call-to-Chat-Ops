# xMatters Post Daily primary on-call from a list of groups to chat ops tool.

Posts the 1 to n number of on-call members from a list of groups to a chat ops tool based on a scheduled xMatters event.

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites

- xMatters account - If you don't have one, [get one](https://www.xmatters.com)!
- Slack / Microsoft Teams / Webex Teams or your favourite chat ops tool.

* This repository uses slack but can be swapped to any chat ops tool of your choice. 
xMatters already has prebuilt steps for Slack and Microsoft Teams. You can find steps for Webex Teams here.

# Files

- [ChatOpsWhosOnCallv4](ChatOpsWhosOnCallv4.zip)

# How it works

A scheduled xMatters event will triggers a Flow that posts to a chat ops tool. 
The Flow gets the on-call resources from a Pipe separated list of groups set as a constant. 
The Flow step creates a string containing the on-call resources for each group in the constant. 
This is posted as a message to a predefined chat-ops channel.

- Supports all group member types (User, Devices, Groups, Dynamic Teams).
- Inactive Users will be skipped and the next on call resource will be used instead.
- Temporary absence will be observed.
- Displays on call resources separated by each shift in a group.
- Will get n number of nested groups and include in the on-call resources list.
- Provides an input for the number of on call resources you would like to post to chat ops tool for each group.
- Wait times and escalation types are included between each on call resource.
- Nested groups with multiple shifts will have shift info included inline.
- Can handle empty groups, empty shifts, and groups with no shifts.
- Include (optionally) a users device in the chat ops message.



_Sample On-Call Posted to Slack:_

<kbd>
    <img src="/media/slack-output.png" width="650px">
</kbd>
<br><br>


_Parent: CAB Approvals Group_
<kbd>
    <img src="/media/groupA.png" width="400px">
</kbd>
<br><br>

_Nested Group: Admin Group_
<kbd>
    <img src="/media/groupB.png" width="400px">
</kbd>
<br><br>

_Nested Nested Group: ABCGroup_
<kbd>
    <img src="/media/groupC.png" width="400px">
</kbd>
<br><br>




__Basic Configuration Steps__:

1. Import the xMatters Workflow.
2. Set xMatters Constant for __Groups__.
3. Configure chat ops tool endpoint.
4. Configure Flow.
5. Create a scheduled xMatters event.


# xMatters Configuration


## Import the xMatters Workflow

1. Download the [ChatOpsWhosOnCallv4](ChatOpsWhosOnCallv4.zip)

2. Follow instructions for [Importing a Workflow](https://help.xmatters.com/ondemand/xmodwelcome/communicationplanbuilder/exportcommplan.htm)



## Set xMatters Constant for __Groups__

1. Click __Chat Ops Who's On-Call__ workflow, then go to __Integration Builder__ tab. 

2. Click __Edit Constants__.

3. Select __Groups__ constant.

4. Set the constant value with a pipe "|" delimited list of xMatters group names to get the primary on call from.

	__Example__: ESD_DevOps|ITSM Management|Admin Group

<kbd>
    <img src="/media/groups-constant.png" width="650px">
</kbd>
<br><br>

## Configure Chat Ops Endpoint.

1. Click __Chat Ops Who's On-Call__ workflow, then go to __Integration Builder__ tab. 

2. Click __Edit Endpoints__.

3. Select __Slack__ endpoint. Alternatively, create a new endpoint for different chat ops tool.

4. Configure authentication.

- [Help with Slack](https://help.xmatters.com/ondemand/#cshid=FlowSlack)
- [Help with Microsoft Teams](https://help.xmatters.com/ondemand/xmodwelcome/flowdesigner/microsoft-teams-steps.htm?cshid=FlowTeams)
- Check xmLabs for Webex Teams Steps

## Configure the Flow


<kbd>
    <img src="/media/Flow.png">
</kbd>
<br><br>

1. Click __Chat Ops Who's On-Call__ workflow, then go to __Flow__ tab. 

2. Click __Chat Ops Who's On Call__ Flow.

3. Configure the existing Slack Step:
	
	a. Double click on the __Post to Channel__ Slack Step

	b. Set the __Channel Name__ you would like to post to.
	
	

	<kbd>
    <img src="/media/Chat-tool.png">
	</kbd>
	<br><br>
	
	c. Ensure message is set to __Merge On-Call > onCall__
	
	<kbd>
    <img src="/media/set-message.png">
	</kbd>

	<kbd>
    <img src="/media/output.png">
	</kbd>
	<br><br>

	d. Set the Endpoint.

4. Ensure Merge On-Call Step is configured.
	
	a. Double click on the __Merge On-Call__ Step

	b. Set the __Groups__ Input to the _Groups_ Constant from the right.
	
	c. Set the number of levels of Escalations you would like to post to chat tool.
	
	d. Optional: Set the _Device Names_ input. 
	
		- Include a Pipe | separated list of xMatters device names. 
		- If left blank, devices will not be included.
		- The first device listed in _Device Names_ input, that is found for an on call member, will be included in the message for that member.
		- If a user does not have the first device, the integration will look for the seconds device and continue until all devices are exhausted.
		- To find the device names in your xMatters environment, go to your devices (under profile) and look at the different device names listed.
		- Includes support for Voice, SMS, and Email devices.

	
	The message will only include one device for each user.
	
	Example: Work Phone|Mobile Phone|On-Call SMS
	
	<kbd>
    <img src="/media/add-device.png">
	</kbd>
	<br><br>
	
	
	<kbd>
    <img src="/media/configure.png">
	</kbd>
	<br><br>
	
	
	

## Create a scheduled xMatters event.

1. Go to __Messaging__ tab.

2. Select __Chat Ops Who's on Call__ messaging form

	<kbd>
    <img src="/media/message-form.png">
	</kbd>
	<br><br>
	
3. Click __Schedule Message__.
	- You will get a warning about no Recipients Selected. Go ahead and press __Send__.
	<kbd>
    <img src="/media/Schedule-button.png" width="500px">
	</kbd>
	<br><br>
	
	
	
4. Set the Scheduled Message Name, Recurrence, Frequency, Start and End Date.

<kbd>
<img src="/media/schedule.png" width="400px">
</kbd>
<br><br>
	
* Keep in mind the time that you schedule the event will influence who is on call. The Flow will get who is on call at the time of the event.
If your shift changes at 12am you will want to scheduled the event just After the shift change. 
Failing to do this will post who WAS on call not who IS on call now.
	

Once you have a scheduled message you will see a new section at the bottom of the messaging section as follows:
	
<kbd>
<img src="/media/view-scheduled.png">
</kbd>
<br><br>



# Troubleshooting

[Get help using Flow designer](https://help.xmatters.com/ondemand/xmodwelcome/flowdesigner/flow-designer.htm)
