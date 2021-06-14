# Receipt Line Status and Purchase order line status

> purchase order status:
> * PENDING_DELIVERY(0)
> * PARTIALLY_RECEIVED(1)
> * FULLY_RECEIVED(2)

> receipt line status
> * NOT_SET(2)
> * PARTIAL(0)
> * COMPLETE(1)


> Receipt status
> * POSTED (1)
> * UNPOSTED (2)


~~~
> short-term
> * RL -> receipt line
> * PO -> purchase order
> * POL -> purchase order line
> * R -> receipt
~~~

## Several facts collected
1. - post R is different comparing with complete RL
2. - POL is a summary of all the RL, 
   1. POL status: POL will be set to fully-received if any of RL associated completed, POL will be set to partially-received, if none of the RL is completed
   2. - POL received quantity: POL received quantity will be the sum of all the RL received quantity
   3. - make the POL logic simple and pure
3. - post only change R's status to posted, this action does not change RL status and POL status, it simply post out a R.
4. - PIC web has toggle in RL of R detail page, when you switch to complete of RL, POL will be fully-received, and all the RL associated will be comleted too
5. - when receive units in forklift, RLs status will be updated base on the comparasion of ordered quantity and received quantity, if received quantity is >= order quantity, the RLs will be completed, and POL will be fully-received


