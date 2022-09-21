# Bresse
Bresse is a Python 3 parametric endpoint service checker that runs ontop Debian Linux. It could run whereever Python 3 (and some dependencies are met) runs well and from where each endpoint under test is reachable. It has just been validated under certain circumstances. Debian 11 and ipv4 network are circumstances.

## Why in the world do you need another endpoint tester ?
In our production system, we have (humans) to be waked up if a system is down while it should be up, and we really all love to sleep/tinker clockwise.


## How it works ?
Bresse is a Python 3 scripts called via a syncrhonous (cron) way. It acts in postitive logic. While beeing an endpoint test for many services it MUST replies OK xor NOK on each service tested for each run. It MUST send an auto test in order to validate cyclic rythm of runs.

Bresse cannot works alone. It MUST be integrated into a cluster of computers. Each computer has to be connected via a different netowk provider in order to test endpoints in a manner that services are reachable from each provider.

Bresse sends an email to a monitoring mailbox at each run. The TO adress SHOULD be bresseN+monitor@domain.com in order to let the same mailbox receive all logs of all bresse from bresse1 to bresseN. N should rely on the number of provider you want to test endpoints from.

BresseN+1 can check the age of the last mail received at monitor@domain.com adressed to bresse[1,N]+monitor@domain.com. If the age is larger than the syncrhonous run rythm plus an opertaionnal margin composed by the resultant of the sum of granular timeout of each test and the reasonable time reserved for the mail path.
## Production ready ?
Yes. Note that we are talking about endpoints. We are glad to test from ou final customer point of vue.

In our production system, we run at least a bresse checker (5 min cycle) on :
  - French mainstream providers
    - free
    - orange
    - Bouygues Telecom
    - SFR
  - European cloud provider
    - Scaleway
    - OVH
    - Azure EU

## What ... endpoint ?
Say we have a mssql server. What do we want our service to serve ?
Anoter question. What is the best test to run ?
  - parametric way
    - server ip (or ns)
    - port
    - user
    - password
    - database
    - request
    - assertion

If the _server_ on the _port_, once _user_ is logged on via the _password_ on the _database_, can handle the _request_ and replies with _assertion_, so, we just have to test if _assertion_ ... asserts. It is the endpoint way to test our service. In our production system, the former client uses the same connection. If a problems occurs with a final user connected by a provider under validation, and the above test asserts well, we can think that the server cannot be faulty.

In the same way, if we have to monitor and eshop. Just take a command on an item, and cancel it. Test it over and over. The eshop works well while the test asserts well.

Endpoint testing doesn't help in case of failure.

## In case of failure ?
Our system is connected via Microsoft 365. And yes, Microsoft 365 is tested via our _bresse_ system too.
Emails are checked by a Power Automate flux. If an email contains string ".NOK" (ie MSSQL1_Service.NOK), the power automate send an approbation to technicians. While the approbation is not overtaken by a technician, Power Automate chat bot spams the Teams on computers and smartphones. The flux runs on a time basis. If that technician is working, if that customer pay for the 365/24/7, if ... whatever you want, it a time basis.

## In case of Microsoft 365 (too big to)fail ?
The positive logic push our solution 
