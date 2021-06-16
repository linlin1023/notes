# Receipt Line Status and Purchase order line status


> purchase order status
> * UNRELEASED(0)
> * RELEASED(1)
> * CANCELLED_UNRELEASED(2)
> * CANCELLED_RELEASED(3)
> * COMPLETE(4)
  

> purchase order line status:
> * PENDING_DELIVERY(0) --when nothing received
> * PARTIALLY_RECEIVED(1)
> * FULLY_RECEIVED(2)

> receipt line status
> * NOT_SET(2)
> * PARTIAL(0)
> * COMPLETE(1)


> Receipt status
> 
> * POSTED (1)
> * UNPOSTED (2)
> 


~~~
short-term
 * RL -> receipt line
 * PO -> purchase order
 * POL -> purchase order line
 * R -> receipt
~~~

## Several facts collected
1. - post R is different comparing with complete RL
2. - POL is a summary of all the RL, 
   1. POL status: POL will be set to fully-received if any of RL associated completed, POL will be set to partially-received, if none of the RL is completed
   2. - POL received quantity: POL received quantity will be the sum of all the RL received quantity
   3. - make the POL logic simple and pure
3. - Post R will change R's status to posted, this action does not change RL status and POL status, it simply post out a R. But it will trigger PO status update, when PO only contains completed POLs and cancelled POLs then PO wil be complete, otherwise PO not complete
4. - When R's status is posted, need to update PO status whenever RL's status change
5. - PIC has RL completion toggle in R detail page, the toggle is POL status toggle, when it switchs to red, POL is partially-received, when it switchs to green, POL is fully-received. and its value will be calculated each time when you load R details. it is a boolean when POL fully-received it will be true and toggle green,  when POL is not fully-received, it will be false and toggle red
   1. - when you switch the toggle to green, POL fully-received  and RL is complete.
   2. - when you switch the toggle to red, POL will be partially-received or pending-delivery depends on POL received quantity. RL will be partial
6. - when receive units in forklift, RLs status will be set base on the comparasion of ordered quantity and received quantity, if sum of all received quantities in RLs >= order quantity, the RL will be completed, and POL will be fully-received, otherwise the RLs will be partial and POL will stay partial-received,



