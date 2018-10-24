---
layout: page
title: How to import an SAP Transport Request with the Transport Management System STMS
description: How to import an SAP Transport Request with the Transport Management System STMS
permalink: /:collection/:path
homepage-weight: 2
---

Please also have a look in our [OnlineHelp](https://help.theobald-software.com/en/) for further information.

In this HowTo we will import the Transport Request for the custom functions that is included in your product folder.
You can find the Transport Request in your product folder or as attachement to this article:

We first unzip and copy the file R900141.ECC into the data folder and the file K900141.ECC into the cofiles folder of our SAP System. (The last 3 digits of the transport numbers may be different in your most recent version that you downloaded !)

In our Testsystem this folders are located under >>  \\SAPServer\c$\usr\sap\trans\

Then we start the transaction STMS and click on ![STMSIcon03](/img/contents/STMSIcon03.png){:class="img-responsive" style="display:inline"}:

![STMS](/img/contents/STMS.png){:class="img-responsive"}

In the next screen we see the import queues in our SAP domain. 
We doubleclick on our system EC5 to see the details of the import queue. 

![STMS02](/img/contents/STMS02.png){:class="img-responsive"}

In the import queue screen we click on Extras -> Other Requests -> Add, to go on with the procedure.

![STMS03](/img/contents/STMS03.png){:class="img-responsive"}

Then we click  ![STMSIcon02](/img/contents/STMSIcon02.png){:class="img-responsive" style="display:inline"}:

![STMS04](/img/contents/STMS04.png){:class="img-responsive"}

We select the transport request we copied...

![STMS05](/img/contents/STMS05.png){:class="img-responsive"}

...and then confirm the request and the attachement to the import queue.

![STMS06](/img/contents/STMS06.png){:class="img-responsive" style="display:inline"}
![STMS07](/img/contents/STMS07.png){:class="img-responsive" style="display:inline"}

Back in our import queue we click on ![STMSIcon01](/img/contents/STMSIcon01.png){:class="img-responsive" style="display:inline"}...

![STMS08](/img/contents/STMS08.png){:class="img-responsive"}

confirm the next screen...

![STMS09](/img/contents/STMS09.png){:class="img-responsive"}

and click Yes to start the import.

![STMS10](/img/contents/STMS10.png){:class="img-responsive"}

the checkmark ![STMSIcon04](/img/contents/STMSIcon04.png){:class="img-responsive" style="display:inline"}
 shows that the import finished successfully.

![STMS11](/img/contents/STMS11.png){:class="img-responsive"}

Attachments 	 -----------------------------------------------

[thtrans.zip (209.76 KB)](/files/thtrans.zip)