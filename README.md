# xMatters Post Daily primary on-call from a list of groups to chat ops tool.

Posts the primary on call from a list of groups to a chat ops tool based on a scheduled xMatters event.

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites

- xMatters account - If you don't have one, [get one](https://www.xmatters.com)!
- Slack / Microsoft Teams / Webex Teams or your favourite chat ops tool.

* This repository uses slack but can be swapped to any chat ops tool of your choice. 
xMatters already has prebuilt steps for Slack and Microsoft Teams. You can find steps for Webex Teams here.

# Files

- [ChatOpsWhosOnCall](ChatOpsWhosOnCall.zip)

# How it works

1. Import the xMatters Workflow.
2. Set xMatters Constant for __Groups__.
3. Configure chat ops tool endpoint.
4. Configure Flow.
5. Create a scheduled xMatters event.


# xMatters Configuration


## Import the xMatters Workflow

1. Download the [Chat Ops Who's On Call Workflow](ChatOpsWhosOnCall.zip)

2. Follow instructions for [Importing a Workflow](https://help.xmatters.com/ondemand/xmodwelcome/communicationplanbuilder/exportcommplan.htm)



## Set xMatters Constant for __Groups__

1. Click Chat Ops Who's On-Call workflow, then go to __Integration Builder__ tab. 

2. Click __Edit Constants__.

3. Select __Groups__ constant.

4. Set the constant value with a pipe "|" delimited list of xMatters group names to get the primary on call from.

Example: ESD_DevOps|ITSM Management|Admin Group

<kbd>
    <img src="/media/groups-constant.png" width="650px">
</kbd>
<br><br>

## Configure chat ops tool endpoint.

1. Click Chat Ops Who's On-Call workflow, then go to __Integration Builder__ tab. 

2. Click __Edit Endpoints__.

3. Select __Slack__ endpoint. Alternatively, create a new endpoint for different chat ops tool.

4. Configure authentication.

- [Help with Slack](https://help.xmatters.com/ondemand/#cshid=FlowSlack)
- [Help with Microsoft Teams](https://help.xmatters.com/ondemand/xmodwelcome/flowdesigner/microsoft-teams-steps.htm?cshid=FlowTeams)
- Check xmLabs for Webex Teams Steps

## Configure Flow


<kbd>
    <img src="/media/Flow.png">
</kbd>
<br><br>

1. 1. Click Chat Ops Who's On-Call workflow, then go to __Flow__ tab. 

2. Click __Chat Ops Who's On Call__ Flow.

3. Configure the existing Slack Step.
	
	a. Double click on the __Post to Channel__ Slack Step


	<kbd>
    <img src="/media/Chat-tool.png">
	</kbd>
	<br><br>


	b. Set the channel Name you would like to post to.
	
	c. Ensure message is set to __Get Who's On Call from List of Groups > onCall__
	
	<kbd>
    <img src="/media/set-message.png">
	</kbd>

	<kbd>
    <img src="/media/output.png">
	</kbd>
	<br><br>

	d. Set Endpoint


## Create a scheduled xMatters event.

1. Go to __Messaging__ tab.

2. Select __Chat Ops Who's on Call__ messaging form

	<kbd>
    <img src="/media/message-form.png">
	</kbd>
	<br><br>
	
3. Click Schedule Message.  
	- You will get a warning about no Recipients Selected. Go ahead and press __Send__.
	
		<kbd>
    <img src="/media/Schedule-button.png">
	</kbd>
	<br><br>
	
	
	
4. Give the Scheduled Message a Name, Set the recurrence and frequency, Start date and when it should end.

		<kbd>
    <img src="/media/schedule.png">
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
