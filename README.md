# ServiceNow Critical Network Incident Notification System

## System Overview

I successfully fixed Uber's broken incident notification system that was preventing critical network incidents from triggering email alerts to the Network Operations team. This system was implemented after a critical network outage in Uber's San Francisco data center went unnoticed for 2 hours, causing widespread service disruptions and affecting thousands of riders and drivers. The incident resulted in significant revenue loss and regulatory scrutiny. The system now automatically sends immediate notifications when critical priority network incidents are created, ensuring compliance with the 1-hour SLA requirement.

## Implementation Steps

### 1. Flow Configuration Analysis

I discovered the flow was inactive and had incorrect trigger conditions. The flow was configured to trigger on medium urgency incidents with assignment groups, but needed to trigger on critical priority network incidents.

### 2. Priority Calculation Research

Using ServiceNow's Priority Lookup Rules documentation, I confirmed that Critical priority (1) requires both Impact=High and Urgency=High to be set on incident creation.

### 3. Flow Activation and Configuration

* Activated the flow from draft status
* Updated trigger conditions to: `category=network AND priority=1`
* Verified the "Send Notification" action was properly configured
* Published the flow to make it active

### 4. Group Name Resolution

Fixed the mismatch between the notification configuration and actual user group:

* Notification was configured for "Network Operations" group
* System had "Networking Operations" group
* Created/verified "Network Operations" group exists and has members

### 5. Testing and Validation

Created test incidents with:

* Category: "network"
* Impact: "1 - High"
* Urgency: "1 - High"
* Priority: Auto-calculated to "1 - Critical"

Added specific test incident INC0010010 which verified that emails were successfully sent to the Network Operations team.

## Architecture Diagram

![System Architecture](Diagram.png)

The diagram shows the complete flow from incident creation through email notification delivery to the Network Operations team.

## How Did You Optimize the System?

To improve the incident routing and notification system, I implemented several optimizations:

**Flow Efficiency:**

* Streamlined trigger conditions to reduce unnecessary flow executions
* Configured the flow to run in background mode for better performance
* Added proper conditional logic to prevent false positive notifications

**Group Management:**

* Standardized group naming conventions for consistency
* Verified group membership to ensure notifications reach active team members
* Configured proper email addresses for all group members

**SLA Compliance:**

* Aligned notification timing with the "Urgency High" SLA requirements
* Ensured notifications are sent immediately upon incident creation
* Added incident priority information to email subject for quick assessment

These optimizations ensure the system is reliable, efficient, and meets Uber's operational requirements for critical network incident response. The solution ensures compliance with Uber's operational requirements for critical incident response.

## AI Scenario

An AI agent could significantly enhance Uber's incident notification system by implementing intelligent routing capabilities. The agent would analyze incoming critical network incidents and automatically route them to the most appropriate available engineer based on their expertise (routing, security, cloud infrastructure), current workload, and time zone. By learning from historical resolution patterns, the agent could identify which engineers resolve similar incidents fastest and prioritize assignments accordingly. For Uber's global operations, this would ensure 24/7 coverage by routing incidents to engineers currently on duty, while considering their skill specialization and current ticket load, ultimately reducing resolution times and improving service reliability.