Auto Ticket Classification using Flow Designer
Project Overview
The Auto Ticket Classification using Flow Designer project is a ServiceNow-based automation solution for a school IT helpdesk. It automatically classifies incident tickets based on keywords in the Short Description and Description fields.
The project reduces manual ticket categorization, improves ticket routing, and provides an automated email notification to the caller.
Problem Statement
The school IT helpdesk receives multiple incident requests daily from students and teachers, including:
Wi-Fi issues
Projector failures
Password problems
Slow computers
Currently, IT staff manually review each request and assign a category. This process is time-consuming and inefficient.
This project automates ticket classification using ServiceNow Flow Designer by analyzing keywords in the incident's short description and description fields.
Objectives
Automatically classify incidents at the time of creation.
Reduce manual effort for IT agents.
Improve ticket routing efficiency.
Implement a no-code and easily maintainable solution.
Automatically notify the caller when a ticket is created.
Business Requirements
The system must:
Automatically classify IT tickets based on the issue description.
Assign Category and Subcategory without manual intervention.
Support dependent choice logic between Category and Subcategory.
Send an automated email notification to the caller upon ticket creation.
Store ticket information in a structured and standardized format.
Support easy maintenance and future scalability.
Technology Used
Platform: ServiceNow
Automation: Flow Designer
Application: Global
Configuration Approach: No-code
Main Table: Incident Workflow
Update Set: Project Update Set
Ticket Classification Logic
Keyword / Issue
Category
Subcategory
WiFi / Network
Network
Wi-Fi
Projector
Hardware
Projector
Password / Login
Access
Forgot Password
Slow / Hanging
Performance
Slow Computer
Data Model
The Incident Workflow table contains the following fields:
Field
Type
Reference / Choices
Number
Auto Number
—
Caller
Reference
sys_user
Category
Choice
Network, Hardware, Access, Performance
Subcategory
Choice
Wi-Fi, Projector, Forgot Password, Slow Computer
Short Description
String
—
Description
String
—
State
Choice
New, In progress, On hold, Resolved, Closed
Assigned Group
Reference
sys_user_group
Assigned to
Reference
sys_user
Category and Subcategory Dependency
The Subcategory field is configured as a dependent field based on Category.
Network → Wi-Fi
Hardware → Projector
Access → Forgot Password
Performance → Slow Computer
This ensures that only the relevant Subcategory options are displayed for the selected Category.
Flow Designer
The main flow is named:
Auto Classify School IT Tickets
Trigger
Trigger: Record Created
Table: Incident Workflow
Condition: Category is Empty
Automation
The flow checks the Short Description and updates the ticket according to the matching keyword.
Wi-Fi Issue
If the Short Description contains Wi-Fi or Network:
Category = Network
Subcategory = Wi-Fi
Projector Issue
If the Short Description contains Projector:
Category = Hardware
Subcategory = Projector
Password Issue
If the Short Description contains Forgot Password:
Category = Access
Subcategory = Forgot Password
Slow Computer Issue
If the Short Description contains Slow Computer:
Category = Performance
Subcategory = Slow Computer
Email Notification
After ticket classification, Flow Designer sends an email notification.
To: Caller Email
Subject: Your Request for the issue has been submitted.
Body: Ticket confirmation message
This provides immediate confirmation to the caller that the support request has been submitted.
Testing
Test Scenario 1: Wi-Fi Issue
Short Description: WiFi not working in library
Expected result:
Category → Network
Subcategory → Wi-Fi
Email → Sent to caller
Test Scenario 2: Projector Issue
Short Description: Projector not turning on
Expected result:
Category → Hardware
Subcategory → Projector
Email → Sent to caller
Validation Checks
The project validates:
Mandatory fields are captured correctly.
Auto-number is generated without duplication.
Category and Subcategory values are stored accurately.
Reference fields resolve correctly to user and group tables.
Email notifications are generated correctly.
Ticket classification works according to the configured conditions.
Update Set
The project uses an Update Set named:
Project Update Set
Initial state:
In progress
After development and testing, the Update Set is changed to:
Complete
The completed Update Set can be exported as XML for sharing or transferring the configuration.
Project Workflow
Student / Teacher
       |
       v
Create IT Support Ticket
       |
       v
Flow Designer Trigger
       |
       v
Read Short Description
       |
       v
Check Keywords
       |
       +-------------------+
       |                   |
       v                   v
WiFi / Network        Projector
       |                   |
       v                   v
Network / Wi-Fi       Hardware / Projector
       |                   |
       +---------+---------+
                 |
                 v
        Password / Login
                 |
                 v
       Access / Forgot Password
                 |
                 v
          Slow / Hanging
                 |
                 v
      Performance / Slow Computer
                 |
                 v
          Send Email
                 |
                 v
        Ticket Confirmation
Advantages
Reduces manual classification.
Provides consistent ticket categorization.
Improves ticket routing efficiency.
Uses a no-code automation approach.
Easy to maintain and extend.
Provides automated caller notification.
Uses dependent choices for better data accuracy.
Future Enhancements
The solution can be extended with:
Assignment automation
SLA tracking
Advanced routing
Predictive intelligence
Additional ticket categories
More automated notifications
Conclusion
The Auto Ticket Classification using Flow Designer project provides an end-to-end automation solution for a school IT helpdesk. It automatically classifies tickets based on the issue description, reduces manual effort, improves response efficiency, and sends automated confirmation emails.
The solution uses ServiceNow Flow Designer and dependent choice fields to provide a structured, scalable, maintainable, and user-friendly no-code implementation.
Project Name
Auto Ticket Classification using Flow Designer
Platform
ServiceNow
Automation Tool
Flow Designer
Approach
No-Code Automation
