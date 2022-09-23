# Bresse
Bresse is a Python 3 _parametric_ endpoint service client (checker).

## How it works ?
Bresse is a Python 3 scripts called via a syncrhonous (cron) way. It acts in postitive logic as a standard client. While beeing an endpoint test for many services it MUST replies OK _xor_ NOK on each service tested at each run. It MUST send DRYRUN.OK on a dry run at each start and as the always first test in order to validate cyclic rythm of runs.

Bresse cannot works alone. It MUST be integrated into a cluster of computers. Each computer has to be connected via a different netowk provider in order to test endpoints in a manner that services are reachable from each provider.

Bresse sends an email to a monitoring mailbox at each run. The TO adress SHOULD be bresseN+monitor@domain.com in order to let the same mailbox receive all logs of all bresse from bresse1 to bresseN. N should represents the number of provider you want to test endpoints from.

## How a test can fail ?
As an endpoint, if you want to test a MSSQL server, a parametric MSSQL client has to ask for a data and test the result like an assertion.
If the data returned is NULL or (in any way) not equal to the expected restult, the endpoint test is failed and then, the system has to send a mail that contains SERVICE_NAME.NOK This test doesn't tell that the server is down. It only tells that an arbitrary endpoint client cannont get the expected data once.

## How a test can pass ?
As an endpoint, if you want to test a LAMP stack, a parametric web client has to craft a request and test the result like an assertion. Say we have an apache server, with PHP and a MariaDB. Creata a php page that ask something in the db when a parameter is given. Call the php page with the request packed with the correct parameter. Is the data is verified ok, then the SERVICE_NAME.OK is sent.

## So what ?
Your service name cannot contains "NOK". You can use a Power Automate to create a flux that :
  - Send an approbation via Teams to all techniciens when the latest email received in the monitor mailbox is a aged over a certain trigger. This tells that a bresse endpoint fails.
  - Send an approbation via Teams to all technicians when the latest mail contains the "NOK" string.
- Send a cyclic message via the Power Automate bot into your working fay/hours, or in the contracted supervision clockwise while the approbation is not taken.
