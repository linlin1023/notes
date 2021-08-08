# BOM


> in old ULT , scan any barcodes, no matter pol is tracked or not,
> then scan location. if PO source is not MMS even though it is tracked, do not create receipt, receiptline and inventoryunit

> new ULT only scan and receive tracked (MMS, PIC when pic.tracked on)

> only receive untracked

> in PIC ReceiptManager to POST a receipt, 
>  
> 1 - compose a complete receipt request :
> 
>  {
>    plantCode
>    userName
>    completeOrderLines: false //default,
>    headers  
>  }
> 

