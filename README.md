# Bresse
Bresse is a Python 3 parametric endpoint service checker that runs ontop Debian Linux. It could run whereever Python 3 (and some dependencies are met) runs well and from where each endpoint under test is reachable. It has just been validated under certain circumstances. Debian 11 and ipv4 network are circumstances.

## Why in the world do you need another endpoint tester ?
In our production system, we have to be waked up if a system is down while it should be up.


## How it works ?
Bresse is a Python 3 scripts called via a syncrhonous (cron) way. It acts in postitive logic. While beeing an endpoint test for many services it MUST replies OK xor NOK on each service tested for each run. It MUST send an auto test in order to validate cyclic rythm of runs.

Bresse cannot works alone. It MUST be integrated into a cluster of computers. Each computer has to be connected via a different netowk provider in order to test endpoints in a manner that services are reachable from each provider.

Bresse sends an email to a monitoring mailbox at each run. The TO adress SHOULD be bresseN+monitor@domain.com in order to let the same mailbox receive all logs of all bresse from bresse1 to bresseN. N should rely on the number of provider you want to test endpoints from.

BresseN+1 can check the age of the last mail received at monitor@domain.com adressed to bresse[1,N]+monitor@domain.com. If the age is larger than the syncrhonous run rythm plus an opertaionnal margin composed by the resultant of the sum of granular timeout of each test and the reasonable time reserved for the mail path.
## Production ready ?
Yes.
In our production system, we run at least a bresse checker on a computer linked by :
  - free
  - orange
  - free pro
  - Bouygues Telecom
  - SFR
