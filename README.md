VoltCare ServiceNow Project

VoltCare provides infrastructure for electric vehicle owners, offering convenient charging points in cities, 
highways, and key locations.Application was created during the developer fast-track seminar.

- Fully realized customized Service Portal for the internal team that includes incident record producer, 
charging station maintenance requests and new hire order guide (That uses 'Order Guide Sequential 
Fulfilment' plugin which helps to start request in appropriate order via designated playbook). 
Additionally, two separate Knowledge Bases are available, one for engineer service instructions and a 
second one for service desk agent activities.

- Mid-Server integration with Azure SQL Database using the JDBC probe plugin that simulates Linux 
server that would be used to manage and run diagnostic scripts on the supported charging stations. 
Seamless data communication between ServiceNow instance and the Azure SQL server.

- Customized dashboards for each company role which includes reports from incident management, 
device maintenance and overhaul cost and operation returns. Includes Performance Analytic 
integration with a custom breakdown to filter recent cost records based on the selected charging 
station configuration item.

- CMDB extendable table that holds records of the charging station devices. Includes related list 
relationships for cost operations and plug management. Features various data and field manipulation 
via scripted methods.

- Fully automated retiring process for the charging station based on the incident record that uses full 
extension of the Process Automation implementation. Flows, subflows and appropriate workflows 
created to navigate the process from the start to finish, including custom JDBC flow ‘Action’ that 
updates devices on the Azure SQL side based on the ServiceNow instance incident outcome.

- CSM implementation for the charging station company in the B2C model. Creation of essential entities 
such as accounts, contacts, consumers, assets, and service contracts, users and groups (agents, 
managers) as well product models based on the ServiceNow data guided setup recommendations and 
adjusting them based on already working setup.

- Fully integrated ‘Case’ creation for the designated service desk agents using ‘CSM Configurable 
Workspace’ that supports compatibility with ITSM (Request, Incident, Problem, and Change 
Management) records using ‘Customer Service with Request Management’ and ‘Customer Service with 
Service Management’ plugins. Thanks to the ‘Case’ creation, consumers will be able to report issues 
with the billing and the devices themselves, as well any dissatisfactory results in the charging process.

- CSM Consumer Service Portal (B2C) implementation to directly provide information and support to 
consumers that will be using the services of the charging stations. Consumers will be able to contact a 
service desk agent if there is a need for support, exclusively request a chargeback in case of the 
unsatisfactory service and monitor request that have been created for them.

- Automated Test Framework tests that were essential in quick creation process for the order guide to 
onboard new employees.

Some notable scripting:
- Catalog Client Scripts ‘EV Check Open Incidents’: we are checking if there are already any incident 
created against variable user input under ‘cmdb_ci’ on the Record Producer ‘EV Box Create Incident’. If 
there is an already open and active Incident, we will clear the variable value and display an error 
message on a page.
- UI Action ‘Diagnose Device’: Form button located on the charging station record available only to the 
role of ‘enginner’. On click it is opening the UI Page ‘diagnostic_page’ in the modal from.
- UI Pages ‘diagnostic_page’: page is opened using the UI Action ‘Diagnose Device’. Content of the page 
is a diagnostic choice selector. When the user will choose and click on ‘Submit’ JDBC call is made to the
database to retrieve the diagnostic log and insert that processed log into the new Diagnostic record. 
The user is then redirected back to the same charging station record.
- Script Include ‘AJAXUtils’: programing functions that are handling dynamic retrieval of the database 
records from server on the Client Side actions for example ‘checkUserID’ function is used in the Order 
Guide to check if the value of the ‘User ID’ already exists under ‘sys_user’ table.
- Scheduled Script Execution ‘EV Box Status Check’: every specified amount of time we are sending a 
JDBC call to the database to check if any of the charging stations ‘state’ field is set to ‘Non-Operational’
in the next step Business Rule ‘EV Box DB Check’ is handling the filtering process of the returned JDBC 
call.
- Business Rule ‘EV Box DB Check’: is handling the processing of the JDBC payload that is created under 
the ‘ecc_queue’ table when the call is made to the Azure SQL database. Payload created is in XML so 
for the ease of use we are changing the content to JSON and filtering directory to retrieve important 
information. In the next step we are updating the ‘operational_state’ of the selected charging device
