## Big Bang integration
* Consider a case where you are working for vintage systems where we are developing ecommerce application in Waterfall model

![Alt text](shots/1.PNG)

* Application is in layered architecture

![Alt text](shots/2.PNG)

* We have team managers
   1. Andy
   2. Brian
   3. Cathy

![Alt text](shots/3.PNG)

* Project has to be finished in an year
* Each team works independently for 9 months and finishes the devlopment

![Alt text](shots/4.PNG)

* Big Bang integrations are error prone, so best solution would be continuos integration (CI).
* The Goal of CI is to inform dev teams about the failures of integration.
* To perform CI different tools started like cruise control and hudson/jenkins
* Need for automated tests/unit tests started at this point.

## Agile way of Software Development

* Agile had added smaller and frequent releases, this needs more aggressive automations than CI.
* Expectation:
    * Automated Pipeline which when developer pushes changes
      => Build/Package code
      => Code Quality and Security Issues
      => Automate test executions with System, Performance, Reliablity, Security
      => Report of the Quality of work done yesterday
    * Customer and Internal Releases every 2 weeks