https://kall.kiwiplan.co.nz/kall/kiwiplan/issueViewer.do?id=6257703   ----> GP Ariba
https://docs.google.com/document/d/1qUFkSk2ZuxvLNsGRVJSFH-JlrQOwuUmUwnOF3yzJExU/edit#heading=h.vg37sg7p0d0e ----> DOC for KALL 6257703

https://kall.kiwiplan.co.nz/kall/kiwiplan/issueViewer.do?id=6252823   ---> UOM



Team,

For G-P we are interfacing to a third party SAP Inventory Management application called Ariba (https://www.ariba.com/solutions/solutions-overview/supply-chain/supply-chain-collaboration) which cannot accept changes to a PO Receipt.  We must send a Delete file backing out the entry of the previous Receipt Line Received Quantity followed by a new Add Receipt with the new received value.

This functionality is the same as what RSS currently has and should be controlled via a parameter just as RSS does, as we have customers which use the existing PIC interfaces as they are now, so we don't want to interrupt their process flow. 


We are currently in the process of writing scripts to pull the data from the various tables to piece together something of a replica of the current PIC output Receipt interface file, but this file will be a Delete record type with the previous ReceivedQuantity value shown as a NEGATIVE value to be removed from Ariba followed by another file with a new Add record type with the new ReceivedQuantity value.

NOTICE, at no point will the "change in quantity", or the "difference between the two values" be sent to Ariba. It will always show the actual Quantity Received - the value typed in by the user. For instance, if the original received value entered = 1000 and it is revealed a mistake was make so a modification is needed, a change will be entered for actual quantity received which = 900. We will then create a Delete record for -1000 quantity received followed by a new Add record with a quantity received of +900.

Also, the VERSION number in the interface record must update with each change. Only the initial receipt record for the receiptline can contain the version=1. The database records reflect the version number change, the interface records must reflect this same change.

Most of the other fields in the interface (with the exception of the Unit of Measure field) are not changing, nor is their order. The Unit of Measure field issue is addressed in Kall #6252823. Our scripts and KMC will change the "Type" field to the more standard, and Ariba required, values of "A"dd, "C"hange (for POs), & "D"elete rather than G and R.




"V"|"T"|"RcptNo"|"RcptLine"|"RcptDate"|"OrderNo"|"AP"|"VendrNo"|"POLine"|"ItemCode"|"ItemCodeDesc"|"Unit"|"QuantityReceived"|"OrderLength"|"OrderWidth"|"ReceivedWeight"|"ReceivedArea"
"2"|"D"|"13"|"1"|"2019/05/02 09:58:04"|"12"|"11"|"20231"|1|"Gluing"|"Gluing"|"TH"|-1000|0|0||0



"V"|"T"|"RcptNo"|"RcptLine"|"RcptDate"|"OrderNo"|"AP"|"VendrNo"|"POLine"|"ItemCode"|"ItemCodeDesc"|"Unit"|"QuantityReceived"|"OrderLength"|"OrderWidth"|"ReceivedWeight"|"ReceivedArea"
"3"|"A"|"13"|"1"|"2019/05/02 09:58:04"|"12"|"11"|"20231"|1|"Gluing"|"Gluing"|"TH"|900|0|0||0






# DOCUMENT  FOR PIC INTEGRATION WITH SAP   KALL 6257703

target: PIC should be able to integrate with SAP when receipt is created/modified/deleted
so that AP system can be notified.

two kinds of integration
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




to configure the parameters for dir
./configure.sh
19





















----------------------------------------------------------------------------------

export const unpostedReceiptsModule = '/unposted-receipts';

export const unpostedReceipts = `/receiving/unposted-receipts`;

if url match with above two, do post receipts action
props.actions.postUnpostedReceipts--->postReceipts in reducers/receiving/unpostedReceipts/actions--->
service.postReceipts

if url not match with above two, do post receipt
props.actions.postReceipt() ----> postReceipt in reducers/receiving/receipt/actions 


    

SCM 284252  --- PIC receipt to handle SAP requirments - Adding installer configuration
Adding the following options in the installer configuration
1. AP integration base dir
---enter the base dir for AP integration (Blank to disable)

2. AP receipt integration mode
--- enter the receipt intgration mode: (R) reversal and reapply
Two configuration entries had been added
1) PICS: Service > External Software Integration Options > AP integration base dir
2) PICS: Service > External Software Integration Options > AP Receipt integration Mode
   


SCM 284768




2
I need to create Map<String, String> from List<Person> using Stream API.

persons.stream()
       .collect(Collectors.toMap(Person::getNationality, Person::getName, (name1, name2) -> name1)
But in the above case, I want to resolve conflict in name attribute by using Person's age. is there any way to pass merge function something around the lines (age1, age2) -> // if age1  is greater than age2 return name1, else return name2 ?

8

To select a person based on its age, you need the Person instance to query the age. You cannot reconstitute the information after you mapped the Person to a plain name String.

So you have to collect the persons first, to be able to select the oldest, followed by mapping them to their names:

persons.stream()
    .collect(Collectors.groupingBy(Person::getNationality, Collectors.collectingAndThen(
        Collectors.maxBy(Comparator.comparingInt(Person::getAge)),
        o -> o.get().getName())));



