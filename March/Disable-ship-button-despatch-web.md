## March
* ### Support KALL
  
>**issue:** 

In Despatch web, when user click the ship button, the web does not diable the button immediately until the shipment result come back, so user can keep clicking on it, and trigger shipment for multiple times in different MapIntegration instances.
>**Side knowledge:**

Usually sites will already be configured to launch 2 instances of MapIntegration when starting service.
The way you can check is by going to the site jini conf folder e.g. /kiwi/services/sites/golden/current/conf/kiwiplan/jini,there are these xml files called mapintegration<number>_launcher.xml, (e.g. mapintgration1_launcher.xml).
Each one of those xml files that is present there should cause another instance of mapintegration to be launched during service startup.
 usually, you'll see that mapintgration1_launcher.xml and mapintegration2_launcher.xml are present, with a couple more that have been changed to mapintegration<number>_launcher.xml.disabled

    enabling and disabling the extra mapintegration instances is just renaming the xml files
    
   when I was trying to replicate the issue, I actually enabled 5 mapintegration instances

so I just made sure mapintegration<1-5>_launcher.xml were all named appropriately (without the .disabled at the end)


then when actually starting services, youll be able to see them start up

looks like this:
Wed Mar 03 10:05:46 NZDT 2021:Group-2:out: * [ MapIntegrationService1@nzdevwaynel ] started @ Wed Mar 03 10:05:46 NZDT 2021
Wed Mar 03 10:05:47 NZDT 2021:Group-3:out:Listening for transport dt_socket at address: 57520
Wed Mar 03 10:05:47 NZDT 2021:Group-3:out:Logging to /kiwi/services/sites/darl/9.53.1112/logs/mapintegration_service2.log.txt
Wed Mar 03 10:05:47 NZDT 2021:Group-3:out:Logging monitoring to /kiwi/services/sites/darl/9.53.1112/logs/mapintegration_service2_monitor.log.txt
Wed Mar 03 10:05:48 NZDT 2021:Group-3:out: * [ MapIntegrationService2@nzdevwaynel ] started @ Wed Mar 03 10:05:48 NZDT 2021


>Related code:


-----edi 
I believe it's the one under GEN -> EE -> ULTDLD
      
      
        Text
      
    
    
    
      kwutils:C                    MAINTAIN PARAMETERS                    04/Thu 15:37
================================================================================
System  Description                    V/M
 GEN    General for many systems
Prefix  Description                    View_Mnt Default_key Many_records_allowed
  EE    Electronic Data Export             M                         Y
Number  Parameter                      Value
 1      Data Type                      ULTDLD
 2      Description                    Dockets
 3      Directory Name                 /KIWI/work/espmain/ultdld/
 4      Last File Number Used          39,994
 5      Script name for File Export    EspRenameDkt
 6      Fixed record length 0=variable 0
 7      File Name (optional)
 8      Layout Version                 S2
(M)ore, (B)eg, (L)ist, (Q)uery, (N)ext, (F)inal, (A)dd, (C)hange,  > E....
    


const askJobsStatus = (loadNumber, emptyJobs) =>
    withLoadingIndicator(webService.isAllowTransferUnits())
     .then( isAllowTransferUnits =>
       withLoadingIndicator(webService.getLoadComment(loadNumber))
       .then( loadComment =>
         withLoadingIndicator(webService.getDespatchJobListTableData(loadNumber, emptyJobs))
         .then(tableData => KP.printBol.open(loadNumber, loadComment, isAllowTransferUnits, tableData))))

    


 select * from DLOADS where despatch_load_id=1141 \G;

LOADING, LOADED, AWAITING_BOL, BOL_PRINTED


  public boolean isAllowTransferUnits() {
    if (getParameters() != null && getParameters().getUnitLoadTracking() != null) {
      return getParameters().getUnitLoadTracking().isAllowTransferUnits();
    }
    
    return false;
  }

  getUnitLoadTracking().isAllowTransferUnits();
  



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

scp 









