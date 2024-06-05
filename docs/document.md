DevOpsEngineeringonAWSCloud
```
# Project:BuildingaHighlyAvailable,ScalableWebApplication

```
Group3:AminaMerić&SelmaImširović
```
Thegoal ofthisprojectistoplan,design,build,anddeployawebapplicationtothe
AWSCloudinawaythatisconsistentwithbestpracticesoftheAWSWell-Architected
Framework.

```
● FirstPhase:
```
**Task1:**

Starting with the first phase, we have planned out architectural design for the
infrastructureandforeverynextphase,wecreateditusingtheLucidCharttool.

**Task2:**

Additionallyweestimatedthecoststhatwewillspendbuildingthewebapplicationusing
theAWS PricingCalculator. IntheAWSPricingCalculatorweaddedalltheservices
thatweusedinourinfrastructurewhichareAmazonPrivateCloud(VPC),AmazonRDS
for MySQLand theAmazon EC2instance.Attheendourestimatedmonthlycostis
55.70USD.

```
● SecondPhase:
```
**Task1:**

In this phase, we first created an Amazon Virtual Private Cloud (VPC) named
"amina-vpc"in the USEast(N.Virginia)/us-east-1region.OurVPCconsistsoftwo
publicsubnetsandtwoprivatesubnets.Onepairofpublicandprivatesubnets(public
and private1)isin theus-east-1a availability zone,while the other pair(public2and
private2)isintheus-east-1bavailabilityzone.

Next, we created an internet gateway and attached it to the VPC to enable
communication with the internet. Then we created a Route Tablefor our VPC.We


added routes tothis RouteTable fortheinternet gatewayandassociatedtheRoute
Tablewithourpublicsubnets.Toallowtheprivatesubnetstoaccesstheinternet,we
createdaNATGatewayinoneofthepublicsubnetsandaddedthenecessaryroutesto
theRouteTableassociatedwiththeprivatesubnets.

AftersuccessfullycreatingtheRouteTables,we createdtwoSecurityGroups:onefor
theEC2instancesandtheotherforthedatabase.Weconfiguredtheinboundrulesfor
these Security Groups to allow the necessary inbound traffic. With this setup, we
successfullylaunchedourVPC.

**Task2:**

In thesecondtaskwelaunchedanAmazonEC2instance.Fortheamazonmachine
Image(AMI)weselectedUbuntu,andtheinstancetypeist2.micro.Forthisinstancewe
selectedthe VPCandsubnets previously created, andattached thesecurity groups
fromtaskone.

Inordertoinstallthewebapplicationanddatabaseonourvirtualmachine,weexecuted
thisscript:

(Scriptcanbefoundinthehelper-scriptsfolder.)


Afterthatwelaunchedtheinstance.

**Task3:**

Lasttaskwas toactuallytestthisdeploymentandtoensurethatwecansuccessfully
accessandnavigatethroughit(screenshotcanbeseenbelow).

**Architecturaldiagramaftersecondphase:**


```
● Thirdphase:
```
Theaimofthisphaseistomakeourapplicationrunnableonseparatevirtualmachines.

**Task1:**

Inthistaskwemodifiedtheinboundrulesinthepreviouslycreatedsecuritygroupthatis
associatedwiththedatabase(MySQLAurora)inorderfortheVPCtobeabletoaccess
theinstancesofthedatabase.

**Task2:**

SecondtaskwasaboutthecreationoftheAmazonRelationalDatabaseusingMySQL
engine. The database instance is called “STUDENTS” and it residesin theprivate
subnetswithinourVPCinordertoensurethatitisnotpubliclyaccessibleandtoensure
thatitismoresecure.

**Task3:**

In this task we needed to establish the Cloud9 environment in order to run AWS
CommandLineInterface(CLI)commands.Weusedthet3.microEC2instancewhichis
configuredwiththeSSH-SecureShellaccessforsecureandreliableconnectionand
alsoourCloud 9 environmenthasaccesstotheRDSMySQLdatabase.

**Task4:**

WiththefourthtaskweprovisionedAWSSecretManager.Wedidthatbyrunningthis
script:

(Scriptcanbefoundinthehelper-scriptsfolder.)

**Task5:**

InthefollowingwemadeanewEC2instanceinthesamewayasthepreviousone,
onlyfortheuserdataweinsertedandexecutedthefollowingscript:


```
(Scriptcanbefoundinthehelper-scriptsfolder.)
```
**Task6:**

Inthistaskwemigratedthedatabase fromtheoriginalEC2 instancetothenewone
whichwecreatedinCloud9.OntheCloud9werunthefollowingscript:

(Scriptcanbefoundinthehelper-scriptsfolder.)

Withthiswe successfullymigratedthedatabaseandmadesurethateverythingworks
properly.

**Architecturaldiagramafterthirdphase:**


```
● Fourthphase
```
Phasefourwasaboutensuringthehighavailabilityandscalability.Becauseofthatwe
launchedtheApplicationLoadBalancer.

**Task1:**

Wecreatedan ApplicationLoadBalancerandconfigureditsname,schema,AZs(two
availabilityzones: _us-east-1a_ and _us-east-1b_ ),securitysettingsandrouting.

**Task2:**

AftercreatingLB,wesetuptheEC2instancebycreatingaLaunchTemplate,selecting
theappropriateAMIandinstancetype,andenablingautoassignedIPv4addressesfor
publicaccess.ThenweconfiguredtheautoscalinggroupbyselectingVPCinsubnets
andattachingLB.

Thissetupensuresthatourwebapplicationispubliclyaccessibleandcandynamically
scaletohandledifferentloads,providinghighavailabilityandscalability.

**Task3:**

WetestedtheapplicationbyperformingsomebasicCRUDoperationsinordertoseeif
everythingworkscorrectlyandfine.

Addingthestudent:


Gettingthestudent’sdata:

**Task4:**

AttheendweexecutedthefollowingscriptonCloud9againsttheloadbalancer:

(Scriptcanbefoundinthehelper-scriptsfolder.)


By this we successfully completed this project that covers various aspects of
architecturedesign,costestimation,webapplicationdeployment,networkconfiguration,
security measure setup, high availability and scalability, and access permission
management.

**FinalArchitecturaldiagram:**

Thegoal andsour focuswastoobtainacomprehensiveunderstandingandpractical
experiencewithAWSservices.


