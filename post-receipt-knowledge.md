Hi all,  below is post receipt related knowledges that I could share to help with your future tasks if related. The code itself is quite straight forward, you could get the work flow easily by read through the code. But you still could refer below content for convinience. 
>Note: If you already familiar with below content, please ignore it =). 


Post receipt is an operation can be done in PIC web. User could post one receipt or multiple receipts to AP system at a time. And user could repost the receipts if there has any updates on the POSTED receipts.


### Process of posting receipt
1. When the user do post operation: 
   1. update the receipt or receipts status to POSTED, 
   2. get Path of SAGE and AP integration,
   3. generate XML file if AP path is populated
   4. generate CSV file if SAGE path is populated
2. Any update of received quantity on posted receipt will trigger re-post receipt
   1. if the delta is not equal to zero, then generate XML report if AP path is populated.  it will have two XML files, one is to reverse the previous received quantity and another is to addd the new received quantity.
   2. if the delta is not equal to zero, then generate CSV report is SAGE path is populated. In the CSV file the received quantity is the delta value between previous received quantity and new received quantity.
   

>Note: Receipt line status will be calculated based on totally received quantity during receive operation, so post receipt will not do any update on purchase order line and receipt line status as they should be updated by any operation that will change received quantity.

### Configuration for posting receipt:
1. run SITE_PATH/bin/configurer.sh.
2. choose the number of PIC service.
3. choose External Software Integration Options.
4. configurer the parameter: 'AP integration base directory', this is for enabling XML file export and path for XML reports.
5. configurer the parameter: 'SAGE integration base directory', this is for enabling CSV file export and path for CSV reports.
6. make sure the paremeter: 'AP receipt integration mode' is "R", which is the only value. "R"  means reversal and reapply.This is for GP Ariba which can not accept delta. we have to send a delete file backing out the entry of the previous receipt line received quantity followed by a new add receipt line with new receive value.
7. SITE_PATH/conf/recentparametervalues.properties this is another place you could check and add above parameters.

   
### Two kinds of integration
* SAGE integration  +/- of the original quantity (existing) (CSV)
    * When SAGE dir is undefined then SAGE CSV file will not be created
    * No change in SAGE CSV file, for receipt modification, the receipt files will contain incremental changes
* SAP integration   complete-reversal of the transaction followed by the new quantity, AP configuration  (XML)
    * Given the AP dir is populated, the XML file will be created
    * the AP receipt integration mode has only one choice R
    * XML file will contain below
      * Receipt:
        * Action Code  : Add or Change
        * Plant code (export action happend in PIC, so use the plant code in PIC)
        * Plant name
        * Truck ID if provided
        * Kiwiplan Receipt Number 
        * BOL if provided
        * Receipt status: 1 for complete or 2 for in progress, Receipt status will be Complete when receipt is sent to AP
        * Receipt status description: Complete or In progress
      * Receipt Lines:
        * Action Code: Add or Delete
        * Receipt line number: Kiwiplan receipt line number
        * Receipt line plane code: Plant code for receipt line
        * PO number: Kiwiplan PO line number
        * Receipt line status: 0-partial (receipt is started but not completed) 1-complete, receipt line will be complete when receipt is sent to AP
        * Item code: Item code
        * Item description: Item description
        * GL code: GL code for item, If you item does not have GL code, this will be populated with GL code from item category
        * Received date time: Received date time
        * Received quantity: Received quantity expressed in the specified UOM
        * Unit of measure: UOM
        * Unit of measure description
        * Received length
        * Received width
        * Receipt line comments
        * Default manual ship to address

### The KALLs for the background knowledge 
1. [6257703](https://kall.kiwiplan.co.nz/kall/kiwiplan/issueViewer.do?id=6257703) 
2. [6252823](https://kall.kiwiplan.co.nz/kall/kiwiplan/issueViewer.do?id=6252823)



   
