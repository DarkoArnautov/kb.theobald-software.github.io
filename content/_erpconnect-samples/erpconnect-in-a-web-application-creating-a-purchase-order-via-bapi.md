---
layout: page
title: ERPConnect in a web application- Creating a Purchase Order via BAPI
description: ERPConnect in a web application- Creating a Purchase Order via BAPI
permalink: /:collection/:path
homepage-weight: 14
---

Please also have a look in our [OnlineHelp](https://help.theobald-software.com/en/) for further information.

Of course, ERPConnect is ready for ASP.NET so you will be able to write really cool web applications with a direct link to SAP R/3.

The following example shows the development process for the ASP.NET/ERPConnect project.

The ERPConnect.dll class library must be added as a reference to the project. The dll will be copied to the bin directory when compiling the project. But you need to add one more dll to your bin directory: librfc32.dll. This one is contained in the rfcsdk provided by the SAP GUI installation (System32 directory).

Attention! The trial version of ERPConnect does not work in a web environment. Please apply for a limited test licence number if you want to use ERPConnect with your ASP.NET project (support@theobald-software.com).

**ASP.NET Example: Creating a Purchase Order via BAPI**

The example below is based on an ASP page that contains several textboxes for the vendor number (txtVendor), the material number (txtMaterial), the quantity (txtQuan), and the plant the vendor should deliver the material to (txtPlant).

Place the following code into the button click event. First of all, we need to establish a connection to the SAP system and create a RFC-Function object (we want to create a purchase order, so we use the BAPI_PO_CREATE BAPI).

<details>
<summary>[C#]</summary>
{% highlight csharp %}
private void Button1_Click(object sender, System.EventArgs e)
{
   R3Connection con = new R3Connection("SAPServer",00,"SAPUser","Password","EN","800");
  
 ERPConnect.LIC.SetLic("LicenseNumber");
  
 con.Open(false);
  
 // Create a RFC-Function object
 RFCFunction func = con.CreateFunction("BAPI_PO_CREATE");
{% endhighlight %}
</details>


The structure PO_HEADER has to be filled in with the following values:

DOC_TYPE -> Order type (NB normal order)<br>
PURCH_ORG -> Purchasing organization<br>
PUR_GROUP -> Purchasing group<br>
DOC_DATE -> Date <br>
VENDOR -> Vendor number

<details>
<summary>[C#]</summary>
{% highlight csharp %}
// Fill header structure
 RFCStructure Header = func.Exports["PO_HEADER"].ToStructure();
 Header["DOC_TYPE"]= "NB";
 Header["PURCH_ORG"] = "1000";
 Header["PUR_GROUP"] = "010";
 Header["DOC_DATE"]= ERPConnect.ConversionUtils.NetDate2SAPDate(DateTime.Now);
 Header["VENDOR"]= this.txtVendor.Text
{% endhighlight %}
</details>

Now the items have to be defined (table PO_ITEMS). All we need is the plant (PLANT) and the material number (PUR_MAT). 
The values for the quantity (QUANTITY) and the delivery date (DELIV_DATE) must be placed in the table PO_ITEM_SHEDULES.

<details>
<summary>[C#]</summary>
{% highlight csharp %}
// Create an Item
 RFCTable items = func.Tables["PO_ITEMS"];
 RFCStructure item = items.AddRow();
 item["PO_ITEM"] = "1";
 item["PUR_MAT"] = this.txtMaterial.Text;
 item["PLANT"] = this.txtPlant.Text;
  
 // Create and fill shedules
 RFCTable shedules = func.Tables["PO_ITEM_SCHEDULES"];
 RFCStructure shedule = shedules.AddRow();
 shedule["PO_ITEM"] = "1";
 shedule["DELIV_DATE"] = ERPConnect.ConversionUtils.NetDate2SAPDate(DateTime.Now);
 shedule["QUANTITY"] = Convert.ToDecimal(this.txtQuan.Text);
{% endhighlight %}
</details>

Now we can execute the BAPI and process the return messages.

<details>
<summary>[C#]</summary>
{% highlight csharp %}
// Exceute Bapi and process return messages
func.Execut e();
this.txtReturn.Text = "";
  this.txtReturn.Text += func.Tables["RETURN"].Rows[0, "MESSAGE"] + "\r\n";
{% endhighlight %}
</details>

The screenshots below show the ASP page and the created purchase order.

![CreatePurchaseOrderIE](/img/contents/CreatePurchaseOrderIE.jpg){:class="img-responsive"}

![CreatePuchaseOrderME23](/img/contents/CreatePuchaseOrderME23.jpg){:class="img-responsive"}

