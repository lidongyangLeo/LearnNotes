## System Diagnostics Demo

Today we Demo System Diagnostics .

when we click on the left menu System Diagnostics. two submenus will appear.

- SQL diagnostics

- log monitor

First when we click SQL diagnostics, this pag	e will appear on the right.

On this page we can see two parts.

**The first part is dataSource info**

datasource name

we can choose datasource to show sql information.

connect to the dataSource userName

datasource url

they can't edit.

**The second part is sql info table**

In this table we can see a lot if SQL information

- Execute count

- Total time

- Max time span

- Transaction【穿咋可深】 count

- Error count

- Effect row count

- Fetch row count

- Last time

There are two buttons in actions.

- View details
- Copy SQL

**When we click the View details button, a detail information page will pop up.**

we can see full sql information.

we can also copy it.

we can also see Last slow view Information

- Max time span 

- Max time occur (er 克)

- Last slow parameters. （per ram ters）

next we can see Last error view information.

if an error occurs,we can see some error messages.

- Last error message
- Last error class
- Last error time
- Last error stack

when we click copy SQL button, we can copy a full sql .

 

table top menu

we can set the time to auto refresh this table.

we can pause and resume (ri'zu: m)this refresh setting.

if this table has a lot of information, so we can click Reset button to clear table.

======================================================

**Log Monitor**

next when we click Log Monitor, this page will appear on the right.

This page will show a table about log information.

- Log Name
- location
- log Path
- log size
- Actions.

click actions, will show

- view log
- Export

when we click View log button, will open new tab page to dispaly the server log in real time .

we can open dark mode or not.

when there are a lot of logs ,we can click clear button,clear log.

we can clear log. 

if you want export log, we can click export button, the log will be exported。

and export log.

 will add log level support later for it. 

now add log level to support it . 

we can change it log level on the web page.

 it will be reflected on the log monitor screen in real time.





===============================================================

**From:** Dongyang Li 
**Sent:** Tuesday, November 9, 2021 9:11 AM
**To:** 752860629@qq.com
**Subject:**

 

**Admin Demo**

when admin login, the left menu will show Settings and System diagnostics.(带个闹死dei可死)

- Instance setting
- External applications
- Global configuration

first the instance settings

this page show instance information.

instance name, type, protocol, host:port, ap iversion, status, actions 。

click actions, we can edit instance information.

the instance name we can change other name.

protocol we can change http or https.

api version, hots port we can change it too.

the instance status we can change active/inactive .

**next External Applications**

now, we only support Community Manager Applications.

this page show Community Manager Application information

name type Desc URL

click actions

we can edit the information

name we can change other name, but Name must be fewer than 50 characters

protocol we can change http/https

url we just need to change host,

port is required, we can change it.

the description is not required, so wo can add it or not.

**next Global Configuration**

now Global Configuration have two tab page.

- Common
- Function ID

**Common**

common Tab Page have four settings.

- rdo.web.auto.refresh.long.interval
- rdo.web.auto.referesh.short.interval
- rdo.web.default.item.per.page.
- rdo.web.session.timeout

autoRefresh long interval defulat value 30 minutes

the task page, depoyment list page and artifacts page use autorefresh long interval

autoRefresh short intertval default vallue 10 seconds

deployment set page and receiver locations page use autorefresh short interval

rdo.web.default.item.per.page

rdo.web.default.item per page.default value is 10.

rdo.web.session.timeout

default value is 1h

the Function Id tab page

this function id is used as the user to run a timer schedule deployment

so ,wo can change it password.

click pen icon

frist inuput current password

input new password

repeat new password

 

================================
Rocket Software, Inc. and subsidiaries ■ 77 Fourth Avenue, Waltham MA 02451 ■ Main Office Toll Free Number: +1 855.577.4323
Contact Customer Support: https://my.rocketsoftware.com/RocketCommunity/RCEmailSupport
Unsubscribe from Marketing Messages/Manage Your Subscription Preferences - http://www.rocketsoftware.com/manage-your-email-preferences
Privacy Policy - http://www.rocketsoftware.com/company/legal/privacy-policy
================================ 

This communication and any attachments may contain confidential information of Rocket Software, Inc. All unauthorized use, disclosure or distribution is prohibited. If you are not the intended recipient, please notify Rocket Software immediately and destroy all copies of this communication. Thank you. 











(?:interface\s)((?:\w+)+\d+(?:/\d+)*)(?:\n\sdescription\s)?(?:\n\sswitchport\s)?([a|t]\w+)?(?:\s\w+\s)?(\d+)?(?:\n)?(?:.+\n)?\s?(dot1x)?