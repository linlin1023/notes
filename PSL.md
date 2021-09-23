enterprise-wide identifier of a store will be its code.


store will need to identify a single "primary plant" that it belongs to.


in an environment with an enterprise locations service, and individual manufactuing installations, 
this "primary plant" is going to be used to determine which nanufacturing dataset the store (and its locations)
beed to be mapped into. For example, if I have two sites, A and B each with their own installations of the manufactuing
software, connected with a single stores and locations sercice, then the shadow tables in dataset A should contain the stores and 
locations belonging to A's plants, and the shadow tables in dataset B should contain the stores and locations of B's plant(s).
Also from a classic perspective, the primary plant is one the attributes of store.







# remove kp-file dependenccy
1. create lib
2. [1.0.0, 2.0.0)  -- so each time the minor upgrade we do not have to change POM 
3. check class path,  before moving, the inventory-tracking-service is mixing using the kp-measure lib and module, currently we purely using the kp-measure lib
   

# unposted receipts 
1. 312146  unposted receipts show :  
   1. in PIC => stores accociated with this plant -> all connection strings for the sores --> for each connection string find all receipts
   2. ult.new
   3. show receipts in PIC and inventory-tracking
   
# more fields 310867

# export XML CSV for receipts
1. XML  &amp; => &   in XML, ==> not a problem when open in browser
2. status ==> POSTED
3. bolNumbers 
4. truckId is always null, no place use it in PIC and ULT ---> I was wondering what is truck ??? put it in report just for same result as original PIC
5. encouter the issue that the forklift-web cannot get order line from PIC
   1. module.addSerializer(Lineal.class, new LinealSerializer());
   2. module.addDeserializer(Lineal.class, new LinealDeserializer());
   3. module.addDeserializer(ArealDensity.class, new ArealDensityDeserilizer())
6. 
7. 

# glCode,  for accounting system
1. write upgrader copy categopry's glCode to its items that do not have a glCode
2. when create a new item, get glCode from category as default, and allow user to edit it
3. when edit glCode in category, provide option to user to propagate this glCode change to its items or not
4. when generate report to accounting system, when an item does not have glCode, get glCode from category.

# KALL stop multiple invoke of shipment, user click multiple times and the button of ship is not disabled
1. print BOL dialog sometimes will show 
2. when the dialog not show, when the user clicks the ship button, it does not stop them from clicking again, util the shipping process is actually complete
3. more than one instances of MapIntegration when start service
4. the way you could check is by going to the site jini conf folder e.g. /kiwi/services/sites/golden/current/conf/kiwiplan/jini
5. in there , these XML files  called mapintegration<number>_launcher.xml (e.g. mapintegration1_launhcer.xml)
6. each one of those xml files that is present there should cause another instance of mapintegration to be launched during service startup
7. usually, you will see that mapintegration1_launcher.xml and mapintegration2_launcher.xml are present, with a couple mroe that have been changed to mapintegration<number>_launcher.xml disabled
8. add .disabled at the end
9. edi file location configuration, GEN-> EE->ULTDLD

rsync -avz ssd@nzmaptiles:/maptiles/routing/australia-osm-gh /kiwi/roadgrids/australia-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/europe-osm-gh /kiwi/roadgrids/europe-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/south-america-osm-gh /kiwi/roadgrids/south-america-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/south-america-osm-gh /kiwi/roadgrids/south-america-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/british-isles-osm-gh /kiwi/roadgrids/british-isles-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/north-america-osm-gh /kiwi/roadgrids/north-america-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/central-america-osm-gh /kiwi/roadgrids/central-america-osm-gh
rsync -avz ssd@nzmaptiles:/maptiles/routing/osm-gh /kiwi/roadgrids/osm-gh


rsync -avz ssd@nzmaptiles:/maptiles/routing/ /kiwi/revisions/$1/
rsync -avz ssd@nzmaptiles:/src/$1/sql /kiwi/revisions/$1/
rsync -avz ssd@nzmaptiles:/src/$1/etc /kiwi/revisions/$1/
rsync -avz ssd@nzmaptiles:/src/$1/bin /kiwi/revisions/$1/

update  DLOADS set  despatch_status = 5 where despatch_load_id = 1141;

update  DLOADS set  despatch_status = 2 where despatch_load_id = 1141;

 public static final PcsLoadStatus PLANNING = new PcsLoadStatus(1, CODE_PLANNING);

  /**
   * Issued
   */
  public static final PcsLoadStatus ISSUED = new PcsLoadStatus(2, CODE_ISSUED);

  /**
   * Loading
   */
  public static final PcsLoadStatus LOADING = new PcsLoadStatus(3, CODE_LOADING);

  /**
   * Complete
   */
  public static final PcsLoadStatus LOADED = new PcsLoadStatus(4, CODE_LOADED);   ---4 will have pop up window to ask the print bol stuff

  /**
   * Despatch
   */
  public static final PcsLoadStatus AWAITING_BOL = new PcsLoadStatus(5, CODE_AWAITING_BOL); --- will skip pop up window

  /**
   * Shipped
   */
  public static final PcsLoadStatus SHIPPED = new PcsLoadStatus(6, CODE_SHIPPED); ----6  no stuff show up in despatch

  /**
   * Billing
   */
  public static final PcsLoadStatus BOL_PRINTED = new PcsLoadStatus(7, CODE_BOL_PRINTED); ---- will have resume loading available

  /**
   * Setup
   */
  public static final PcsLoadStatus SETUP = new PcsLoadStatus(8, CODE_SETUP); -- not show up in despatch

  /**
   * Ready
   */
  public static final PcsLoadStatus READY = new PcsLoadStatus(9, CODE_READY);


  # KALL 6490249 shipped loads return to loaded
 find u/kiwi/services/sites/kcty/current/logs/.  -type f -exec grep LoadNotFoundException /dev/null {} +
 find ./  -type f -exec grep "load '3842' not found" /dev/null {} +


 # Prompt when edit category
   

2. in the maintenance page of item category
  2.1-new item category
    --set an item category as trackable, so it will provide a default for all items in the system
    --then all future items created will inherent the new stocking policy
    --
  2.2-chagne item category
    --set an item category as trackable, so it will provide a default for all items in the system
    --a dialog should pop up to confirm whether the user want to apply the new stocking policy to all existing items





Given the material planner finished editing the item category, when clicking the 'Save' button, then the action will no longer have any confirmation prompt regarding these fields.



Technical Info

In legacy PIC, the "Tracked" stocking policy already exists for the purpose of MMS sheet board. Investigate into where and how it is being used. Look out for any potential side effect if any PIC items also start having "Tracked" stocking policy.
Tracked, Stocked, and Un-stocked inventory will be reported in a slightly different fashion.

Tracked will most likely to be reported inventory by inventory, with an aggregation of the totals
Stocked will be reported with an aggregation of the totals
Un-stocked will not be reported.


Different tiers of stocking policy and be upgraded in "one direction".

"Tracked" can become "Stocked" without being lossy. "Stocked" cannot become "Tracked" without some compromise.
"Un-stocked" cannot become "Stocked" or "Tracked" without some compromise (literally, nothing to show here... move along)


The change does not propagate to the actual inventory, though when come to reporting, report all inventory based on the current item stock policy. The data may look strange but it is what it is.


# add pic.tracked
313701-add pic.tracked

inventory-tracking-service disable the scanning of untracked

the item type & category tracked stocking policy hide behind the pic.tracked feature

for tracked, we need to distinguish them by licence, 
if pic.tracked on, the tracked can from PIC ESP MMS
if pic.tracked off, the tracked can only from MMS

enable/disable the scanning of PIC/ESP tracked barcode based on the new licence , 

Scanning of MMS tracked barcodes should always work.

TODO clarify - Should we disable the selection of MMS boards when creating PO/POL in PIC

are we allowed to create another category under type sheets ?  -

language translation issue

      <entry id="item-non-mms-tracked">Unsupported scanning of non MMS Tracked inventory for %(itemDesc)s</entry>
      <entry id="item-non-tracked">Unsupported scanning of non Tracked inventory for %(itemDesc)s</entry>

ScanValidationException("ITEM_NON_TRACKED", message,


    throw new ScanValidationException("ITEM_NON_MMS_TRACKED", message, Parameter.of("itemDesc", itemDesc));

# badge 
Badge 


unpost receipt number in pic 
select count(distinct r.id) from receipt r, receiptline rl, purchaseorder po, purchaseorderline pol where r.id = rl.receiptId and rl.receivedQuantity >0 and rl.purchaseOrderLineId = pol.id and pol.purchaseOrderId = po.id and r.status = 2 and r.plantId = 1 and po.source;

MMS


if ult.new, get the unposted receipt count from the new system


select count(distinct r.id) from inv_receipt r, inv_receipt_line rl, purchaseorder po, purchaseorderline pol where r.receiptId = rl.receiptId and rl.receivedQuantity >0 and rl.purchaseOrderLineId = pol.id and pol.purchaseOrderId = po.id and r.status = 2 and r.plantId = 1 and po.source;


includePic true  & includeMms false
  po.source != mms  ===> ESP and PIC

includeMms true & includePic false
  po.source = mms   =====> mms only

  private PurchaseOrderLine validateAndGetPurchaseOrderLineIfExists(String plantCode, String purchaseOrder,
                                                                    int purchaseOrderLine)
      throws ScanValidationException
  {
    PurchaseOrderServiceClient purchaseOrderService = getPurchaseOrderService(plantCode);

    PurchaseOrderLine orderLine = purchaseOrderService.getPurchaseOrderLine(
        purchaseOrder,
        purchaseOrderLine,
        plantCode).orElse(null);

    if (orderLine == null || orderLine.getPurchaseOrderStatus().equals(UNRELEASED)) {
      String message = "Unable to find PO " + purchaseOrder + " line " + purchaseOrderLine;
      logger.error(message);
      throw new ScanValidationException(
          "PURCHASE_ORDER_LINE_NOT_FOUND",
          message,
          Parameter.of("purchaseOrderNumber", purchaseOrder),
          Parameter.of("purchaseOrderNumberLine", purchaseOrderLine));
    }
    return orderLine;




  @Override
  public Optional<PurchaseOrderLine> getPurchaseOrderLine(String purchaseOrderNumber, int purchaseOrderLineNumber, String plantCode) {
    HttpUrl httpUrl = getDefaultHttpUrlBuilder()
        .addPathSegment("v1").addPathSegment("purchase-orders")
        .addEncodedPathSegment(purchaseOrderNumber)
        .addPathSegment("lines")
        .addEncodedPathSegment(String.valueOf(purchaseOrderLineNumber))
        .addQueryParameter("plantCode", plantCode)
        .build();

    Request httpRequest = new Request.Builder().get().url(httpUrl).build();
    return client.withHandlerOptional(httpRequest, PurchaseOrderLine.class, getDefaultErrorHandler());
  }


# capture bol number
capture bol number 


- endpoint for capturing BOL number already exists in inventory-tracking-service, but it needs changing so that the BOL number is passed as the request body, not a query param
- probably need an endpoint in the BFF to delegate on to the existing endpoint in tracking service
- clear receipt from front-end storage after setting the BOL number, but only that one receipt (the current active tab on the receipt summary screen)



84088-1-1231-1

84080-1-23423-1

PIC.VIEW_PIC_RECEIPTS_ON_UNPOSTED_RECEIPTS

pic.tracked



84092--PIC
84093 -- PIC --AMERICAN INK ....

Vuteq/Chipboard Partition --- stock
125C ---- tracked
100096152--- non-stock


# hide receive button when all lines are trackded
|| props.hasNewUltFeatureLicense

v1/plants/{plantCode}/items

  @GetMapping(produces = APPLICATION_JSON_VALUE)
  @ResponseBody
  public List<GetItemDto> getItemDtos(@PathVariable String plantCode, @RequestParam Collection<String> itemCodes)

    result.poLinesTableData.webTableRowData.


http://localhost:8081/pic/v1/plants/1/items/plant-items-by-item-codes?itemCodes=Vuteq

[09:52] Bert Huang
    but, Linlin Pan check if you're able to reuse the existing /v1/plants/{​​​​​​​​plantCode}​​​​​​​​/items endpoint instead of creating a new one
​[09:52] Linlin Pan
    ok,
​[09:53] Bert Huang
    since you're turning an existing optional itemCode into an optional "list" of item codes, the contract should be non breaking so long you keep the query param name the same
​[09:54] Bert Huang
    and adding stockPolicy field onto the PlantItem object should also be non-breaking
​[09:55] Bert Huang
    and Hao 'Jesse' Jiang, once Linlin get that endpoint into PIC, we can potentially go for the more permanent implementation, instead of relying on isNewULTLicenced to toggle between checking PO Source === MMS and hasPOLContainTracked, we can most likely switch completely over to just check the POL containing tracked
​[09:56] Bert Huang
    given that we can query plantItems in bulk instead of in a loop
​[09:57] Bert Huang
    remember, there is a task down at the bottom of the queue to "remove ult.new licence"
​[09:57] Bert Huang
    if we can help it, we should think of ways to reduce the amount of these licence checks, so save our future self from having to untangle it later smile
(3 liked)

# new receipt summary screen


stocked and tracked and pic source (mms and non-stock will not have unit's information)

mms 
select * from inventory_item_desc where name = "83613-1-1-1";
select * from inventory_unit where inventory_item_desc in (211070) \G;;

insert into inv_receipt_line_unit (receiptLineUnitId, lastUpdated, lastUpdatedBy, receiptLineId, barcode, quantity, quantityUom, ) VALUES (:receiptLineUnitId, :lastUpdated, :lastUpdatedBy, :receiptLineId, :barcode, :quantity, :quantityUom)

{
    "data": [
        {
            "number": 2,
            "supplierName": "Michigan Packaging",
            "receiptLines": [
                {
                    "number": 1,
                    "purchaseOrder": "84084",
                    "purchaseOrderLine": 1,
                    "itemDescription": "MARSHALL & BRUCE JOB # 139516",
                    "orderedQuantity": 20200,
                    "receivedQuantity": 100,
                    "units": [
                        {
                           
                        },
                        {
                            "lastUpdated": "2021-05-04T08:18:15Z",
                            "lastUpdatedBy": "admin",
           
                 "itemCode": "MARSHALL & BRUCE  JOB # 139516",
                            "itemDescription": null,
                            "itemCategoryCode": "Board",
                            "itemTypeCode": "2",
                            "owningPlantCode": "1",
                            "storeCode": "1-1",
                            "storeNumber": 1,
                            "locationCode": "LOC2",
                            "creationDate": "2021-05-04T08:18:15Z",
                            "barcode": "84084-1-200-1",
                            "qualityDisposition": "AVAILABLE",
                            "quantity": {
                                "amount": 200,
                                "uom": "Unit"
                            },
                            "costPer": {
                                "amount": "488.2900",
                                "uom": "Thousand"
                            },
                            "valuePer": {
                                "amount": "488.2900",
                                "uom": "Thousand"
                            },
                            "intendedOrder": null,
                            "intendedOrderPlantCode": null,
                            "purchaseOrder": "84084",
                            "purchaseOrderLine": 1
                        }
                    ]
                }
            ]
        },
        {
            "number": 3,
            "supplierName": "Michigan Packaging",
            "receiptLines": [
                {
                    "number": 1,
                    "purchaseOrder": "84084",
                    "purchaseOrderLine": 1,
                    "itemDescription": "MARSHALL & BRUCE JOB # 139516",
                    "orderedQuantity": 20200,
                    "receivedQuantity": 200,
                    "units": [
                        {
                            "lastUpdated": "2021-05-04T07:51:09Z",
                            "lastUpdatedBy": "admin",
                            "itemCode": "MARSHALL & BRUCE  JOB # 139516",
                            "itemDescription": null,
                            "itemCategoryCode": "Board",
                            "itemTypeCode": "2",
                            "owningPlantCode": "1",
                            "storeCode": "1-1",
                            "storeNumber": 1,
                            "locationCode": "LOC1",
                            "creationDate": "2021-05-04T07:51:09Z",
                            "barcode": "84084-1-100-1",
                            "qualityDisposition": "AVAILABLE",
                            "quantity": {
                                "amount": 100,
                                "uom": "Unit"
                            },
                            "costPer": {
                                "amount": "488.2900",
                                "uom": "Thousand"
                            },
                            "valuePer": {
                                "amount": "488.2900",
                                "uom": "Thousand"
                            },
                            "intendedOrder": null,
                            "intendedOrderPlantCode": null,
                            "purchaseOrder": "84084",
                            "purchaseOrderLine": 1
                        },
                        {
                            "lastUpdated": "2021-05-04T08:18:15Z",
                            "lastUpdatedBy": "admin",
                            "itemCode": "MARSHALL & BRUCE  JOB # 139516",
                            "itemDescription": null,
                            "itemCategoryCode": "Board",
                            "itemTypeCode": "2",
                            "owningPlantCode": "1",
                            "storeCode": "1-1",
                            "storeNumber": 1,
                            "locationCode": "LOC2",
                            "creationDate": "2021-05-04T08:18:15Z",
                            "barcode": "84084-1-200-1",
                            "qualityDisposition": "AVAILABLE",
                            "quantity": {
                                "amount": 200,
                                "uom": "Unit"
                            },
                            "costPer": {
                                "amount": "488.2900",
                                "uom": "Thousand"
                            },
                            "valuePer": {
                                "amount": "488.2900",
                                "uom": "Thousand"
                            },
                            "intendedOrder": null,
                            "intendedOrderPlantCode": null,
                            "purchaseOrder": "84084",
                            "purchaseOrderLine": 1
                        }
                    ]
                }
            ]
        }
    ]
}



# POST receipt 
## old process for post receipt 
    old post -receipt process:

1 - compose a complete receipt request : receipt numbers/ bolnumber/ plant code (for complete order default to false)
{
	plantCode
	username
	completeOrderLines: false ///default  ,updateOrderLines in action below
	headers [
          {
		bolNumber
		receiptNumber	
	  }
	  {
                bolNumber
                receiptNumber
          }]
}
compose string of receipt numbers while doing loop
2 - compose message with plantCode and receiptnumbers string
    "successfully post receipts to AP. plant code = , receipt numbers = " 
logger.debug

3- compose message when fail
     "Failed to post receipts to AP. plant code = , receipt numbers = , response code: "
logger.error

in receipt manager
4- loop each receipt header,
   4.1- BOL_MAX_LENGTH = 80, if trimmed bolNumber length exceed this length return error information with (ResponseCode.BolLengthExceeded

5- create action, set receiptheadervalues which contain user and receiptheader and isCompleteOrderLines

6- get receipts from DB by receiptnumbers, update receipts 
7- loop each receipt
  7.1- assgin already complete flag and set receipt status to complete----
  7.2- get bolNumber passed in in the receipt header, compose with the already exist receipt bolNumber to a new bolNumber, when already complete true, and the bolNumber does not equal to the receipt already exist bolNumber, if already complete is not true or bolNumber equals to the receipt already exist bolNumber, just overrite it ( need to trim it to max width 80)
  7.3- set lastUpdatedBy and save to database
 
8- after update receipt begin to update receipt line and order line if specified ----

9- loop through receipt lines and update each receipt line' status to COMPLETE and lastUpdatedBy to the current user.
   9.1- get purchase order line from each receipt line, and through order line get the purchase order, if purchase order status is not COMPLETE, remember the purchase order id in a set(avoid replicate purcase order id)
   9.2- if purchase order line deliever status is not fully-received and updateorderlines flag is true, we need to update orderline's deliver status to fully-received and lastUpdatedBy 

10- began to update purchase order, update purcahse order as COMPLETE if all order lines are FULLY_RECEIVED or CANCELLED,

11- get all the receiptlines of all receipts
12- send information to MMS to finalize purcahse order lines
  12.1- loop through each receipt line 
    12.1.1- get order line from receipt line and check source of order line and order line status is fully received, we need to send this order line information to MMS to finalize them




 PIC system receipt status
  
  /**
   * Initial status, which means receipt is NOT started. 0 in DB.
   */
  UNRECEIPTED(0), 
  
  /**
   * Complete, which means receipt is done and posted to AP. 1 in DB.
   */
  COMPLETE(1), 
  
  /**
   * In progress, which means receipt is started but NOT completed. 2 in DB.
   */
  INPROGRESS(2);


NEW ULT system receipt status

  POSTED(1), NOT_POSTED(2);


  


 1- for generating XML CSV files, system will generate files depending on the configuration of paths,
configuration file is: SITE_SERVICE_PATH/conf/recentparametervalues.properties
XML path config: (if not configured, will not generate any XML file)
integration.AP_INTEGRATION_BASE_DIR=/kiwi/services/integration/valley81
CSV path config: (if not configured, will not generate any CSV file)
integration.INTEGRATION_BASE_DIR=/kiwi/services/integration/valley81
2- for the area column in the CSV file, the value is got by (QuantityReceivedlengthwidth)/1000000
3- glCode can be found in iteminplant
4- user can customize the template of CSV, steps for changing template of CSV
4.1- create directories SITE_SERVICE_PATH/conf/kiwiplan/pics/integration/schema
4.2- copy the customized template here. I have uploaded the template file in JIRA, you could make some changes in the template file before copy to the path to see if it changes format of the generated CSV file


need to ask product owner or tech leader
1-what is density of item (in pic, plantItem model has a field arealdensity, it is used to calculate sheets weight, is it still in use and why iteminplant table both do not have it.)
2-glCode meaning and usage (can check in iteminplant table in database)



  UNRECEIPTED(0), 
  COMPLETE(1), 
  INPROGRESS(2);


  POSTED(1), NOT_POSTED(2);


poline delivery status
public enum POLineDeliveryStatus implements PICStandardEnum{
  PENDING_DELIVERY(0),
  PARTIALLY_RECEIVED(1),
  FULLY_RECEIVED(2);

receipt line status
public enum ReceiptLineStatus {
  NOT_SET(2), PARTIAL(0), COMPLETE(1);
7445-1

poline delivery status 

1. - post is different thing compare with complete of RL

2. - POL is a summary of all the RL, any RL is completed , POL to fully-received, no matter of the quantity 

3. - post only change receipt status to posted



# UOM in receipt summary screen
Count
Lineal
Area
Volume
Weight


# re-export receipt 
old PIC

receipt has version  when created, it is 0, when edit the receiptline, it will not change, when you edit bol it will not change


when change bol, the version of receiptline will not change

after post the receipt, you change bol or receipt line(mainly change received quantity), the version of receipt will not change

when you export the recepit, its version of receipt will bump up



I have a question regarding the version on recepit and recepit line:
 Do we need the version information on receipt and receipt line table in new ULT? cause the names of CSV and XML files of recepit report in PIC have been using the version of receipt line in PIC.

A- In the content of XML and CSV there is NO version information receipt line.
B- In the content of CSV, there is column named "V" which is default as 1 and never change during post/repost
C- In the name of CSV or XML file, we have format like below
   6.1- post(first time post)  : 
             	RYYYYMMDD_RECEIPTNUMBER_1_0.csv / RYYYYMMDD_RECEIPTNUMBER_1_0.xml  (1 and 0 is default)
            eg. R20210825_7469_1_0.csv/R20210825_7469_1_0.xml
   6.2- re-post(edit received quantity of any receipt line in POST recepit will automatically trigger repsot)
		RYYYYMMDD_RECEIPTNUMBER_LineNumber_ReceiptLineVersion.csv 			  
                RYYYYMMDD_RECEIPTNUMBER_LineNumber_ReceiptLineVersion.xml
	    eg. R20210825_7469_1_3.csv (.xml)  which means re-post for changing recepit line 1 and current version of receipt line 1 is 3(version 1 or 2 of this receipt line would not have been posted to AP system if those changes happened before posting the receipt).

In PIC, the way it maintains the versions of recepit and receiptline
1- when firstly create recepit and recepitline, the versions of them are initialized to 0;
2- Each time the user edit recepit line(not matter in UNPOSTED or POSTED recepit), the version of the recepit line will bump up by 1;
3- For receipt only when you post it, it will bump up by 1 ( from 0 to 1), editing recepitline or bol will not bump recepit version.
4- In POSTED receipt, the user edit any recepit line, it will re-post automatically
5- When you re-post, the recepit will not bump up version.
6- The recepit_audit and receiptline_audit will record all the change history(you could find all the versions here), in new ULT, we do not have these two tables. do we need to add them
7- when you delete receiptline, version will bump up one for receiptline and the receivedQuantity will be 0,
---------------------------------------------------------------------------------------------------
UOM test using different quantity, ---done,  quantity is right
ReceivedArea  ----- when R csv, is the remain one

when receiving some line receveid quantity is zero how to deal with it during creating system    
the grain quantity passaround through system or not the grain amount (post/repost)


when flick the receipt status and change bol  in old PIC not repost, need test again

use same recepit in old PIC and new ULT contain length and width information

@Test 
all the java set operation  ----

consider bol number process in receiptController


NEW ULT
test poline 
84092-2      ----- 242  231 232 241  

84085-1-8   ------  251
84126


save button need to check bol and receipt line change


test with the item has length and width density in old PIC and new ULT, and test the change of POSTED recepit



----

if old pic has delete receipt line funciton for UNPOSTED POSTED receipt, and 
for POSTED recepit will it be posted and how the file name goes and how the content goes 



-----

CSV -> type R or G, receivedQuantity is the difference, but the area is calculated by the new receivedf quantity, recpdate is the receiptline

 lastUpdated time



alter table inv_receipt_line add column version int(11) default 0 not null after id


alter table inv_receipt_line change version version int(11) not null

        
             




# support workflow


workflow of support

1- Work on Issue to assign yourself

2- left side --> email this issue (who raised the KALL, PO, SM, TL)

3- CC to me if you want to know

4- CASE A : Lack of info, (dataset licence)
     - email this issue, tell what you need
     - change tier from 3 to 2
     - assign by ticking the box at the end of email form
   CASE B : workaround, on live site data clean
   
     - Email back answer for question
     - assign issue back
     - change tier to 2
     - choose explatned situation
   CASE C : Actual bug
     - double check in team SM TL
     - email them let them know we need SC to fix it
     - do not promise anything
     - edit this issue change type from support to fault, click save
     - click pool for Dev/PM (danger, will remove KALL from tier 3 queue)
     - Simulation KALL keep at tier 3
     - do not spent for more than 2 days (find any related kall, provide script and logging)

5- Priority
     P1 = emergency, need to be fix in 4 hours
     P2 = 2-3 days
     P3 = ASAP, relax, 

6- Do not unassign to yourself without doing any effort and providing any result

7- the person raised KALL happy with your solution 
8- finish survey 


test receive, post and repost

Note: Post and Repost can only be done in PIC

POs for test: 
84092  receive/post/repost in PIC  -  normal PIC PO
84085  receive in ULT,  post/repost in PIC  -  MMS one, has length width information,  
84126  receive/post/repost in PIC  - normal PIC PO, each line has different UOM, to test quantity

Make a snapshot 1 of database atm
in PIC: (after each operation, rename file to POnumber-case-x-linenumber-... just to recogonize the case number and po number)
case 0 ==> all 3 POs, receive each line with 20 amount for all lines, bol is case0 and POST it
case 1 ==> all 3 POs, Change line 2 , 4 each add 10 amount, bol is case1, repost
case 2 ==> only with 84085, change line 2 add 17, 4 reduce 15 amount, bol is case2, repost 
case 3 ==> only with 84085, change line 2 ,4 reduce 1 amount, bol is case3, repost

IN new ULT: restore the database with the snapshot 1
repeat case 0 - case 3

----------------------

issues: 
XML:
  number in receipt line - fixed
  receivedQuantity in recepit line 

  status of receipt line (calculation of status is different, need to restore and test to see if NEW ULT make sense)


for delete receiptline need to be tested in original PIC and new ULT

  






# test upgrader
1- make DB clean 
2- create dbs. and import 9.20 dataset for valley2

3- active software  550   gJ44148
4- xlmain change database name and password
5- create inv_xxx tables
5- upgrade mes to 9.72.1050
4- upgrade map to 9.72.1
6- get 9.72.1054 installation
7- check inv_recepit_line no version column
8- run installer to upgrade the site
9- check inv_receipt_line has version column


     
     for the SingleInstallerInstance you'll need to build kp-tools-external and copy the jar to the dist directory

[19/10/2020, 16:36] Bert Huang
    for configurer.xml.installertemplate its easier if you just modify the configurer.xml inside the template directory


# DDL for PSL
Plants dual maintenance
 1. machine need plant in PCS,
 2. Technicians need to create plant correctly in PCS

take s over the data model in PCS. migrate from manudacturing DB to stores and locations

installation with manufactuing triggers the stores and location migrating(e.g. Stora DSSmith)

PIC : taken plants
Manufacturing take plants, stores and locations

Regarding stores

store number unique within a site

sore code  = plant code + store number only for upgrade data migration


caller has no concept of site Code, they might need tp pass plantcode

plant code enterprise unique

API -- caller pass plantCode

location code only unique within a store

location barcode global unique identifier


KALL 6182212

6174200


invmenu --- classic functions 

store code itself will be unique in the global, the store number is unique within the installation, 
,

plant code > installation code > store number  then store record

installation_code + store_number will be globa unique


in the discussion on 17/7/2021,  the storeCode(for upgrade: plantCode + storeNumber),  this means when we upgrade old site, we grab plant code to generate store code
the upgrader should be part of the data migration

for now we assume the site is newly set up , os the store table wil be populated by people











