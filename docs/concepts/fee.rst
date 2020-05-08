Fee Model
=========

The details of this chapter are as follows:

-  Each can obtain data on the latest traded prices. The newly listed
   pairs take the initial prices as the latest traded prices

1. Invalid order
----------------

**Fee conditions**

When the order is cancelled or expires, it has not been partially
filled, i.e. the order quantity and the remaining quantity are equal

**Fee priority**

Pay with okt first and use other cryptocurrencies when the amount of okt
is insufficient

**Fee rules**

1. Handle the invalid order first and return tokens to the account
2. If okt balance in the user’s account is sufficient, the corresponding
   amount of okt is deducted from his account balance as a handling fee
3. If the user's okt balance is insufficient:

   3.1 If the cryptocurrency locked by the order is okt, all okt in his
   account is deducted as a handling fee.

   3.2 If the cryptocurrency locked by the order is not okt, such as
   acoin, the corresponding amount of acoin is deducted after
   calculation at the latest traded price of acoin/okt (fee/acoinPrice);
   if the amount of acoin is not enough to pay the fee, the total
   remaining balance is deducted.

**Fee parameter references**

In order to encourage users to use and hold okt, the handling fee is
discounted when paying in okt (80% off)

+-------------+-------------------------+--------------+
| Operation   | Pay in non-okt          | Pay in okt   |
+=============+=========================+==============+
| Cancel      | equivalent to 0.01okt   | 0.002okt     |
+-------------+-------------------------+--------------+
| Expire      | equivalent to 0.01okt   | 0.002okt     |
+-------------+-------------------------+--------------+

2. Execute an order
-------------------

**Fee conditions**

When the order is executed, a certain amount of fee is charged in
proportion to the traded amount

**Fee priority**

Pay with okt first and use other cryptocurrencies when the amount of okt
is insufficient

**Fee rules**

1. Execute the order first. Remove the cryptocurrency sold and add the
   cryptocurrency bought in the user’s account
2. Calculate the total number of okt equivalent to the order price at
   the traded price: if the trading pair is acoin/okt, oktAmt = volume
    *traded price of the order; if the trading pair is acoin/bcoin,
   oktAmt = volume  *\ traded price of the order  \*bcoin\_okt price
3. If the payment is made in okt, feeNative=oktAmt\*feeRate
4. Check whether okt balance in the user’s account is sufficient, and if
   it is sufficient, deduct the corresponding amount of okt from his
   account balance
5. If okt balance in the user's account is not enough to cover the
   handling fee, the tokens received by the user after the order is
   executed are directly deducted proportionally

**Fee parameter references**

In order to encourage users to use and hold okt, the handling fee is
discounted when paying in okt

+-------------+------------------+--------------+
| Operation   | Pay in non-okt   | Pay in okt   |
+=============+==================+==============+
| Deal        | 0.1%             | 0.04%        |
+-------------+------------------+--------------+

Other fees
----------

+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
| Module         | Order                         | Deposit   | System Fee Rate                                                                       | Business Fee Rate                              |
+================+===============================+===========+=======================================================================================+================================================+
| Election       | Create validator              | Yes       | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Edit validator information    |           | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Delegate                      | Yes       | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Undelegate                    |           | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Change delegation             | Yes       | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
| Distribution   | Modify distribution address   |           | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
| Governance     | Initiate proposal             | Yes       | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Deposit proposal              | Yes       | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Vote on proposal - others     |           | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Vote on proposal - DexList    |           |                                                                                       | 0%                                             |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
| Order          | Place order                   | Yes       | 0                                                                                     |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Cancel order                  |           |                                                                                       | non-OKT: equivalent to 0.01OKT OKT：0.002OKT   |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
| Token          | Activate Listing              |           |                                                                                       | 100000                                         |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Increase supply               |           |                                                                                       | 2000                                           |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Burn                          |           |                                                                                       | 10                                             |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Freeze                        |           |                                                                                       | 0.1                                            |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Transfer                      |           | 0.0125                                                                                |                                                |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+
|                | Batch transfer                |           | n\*0.01 \| \| \| \| Issue \| \| \| 20000 \| \| \| Transfer ownership \| \| \| 10 \|   |
+----------------+-------------------------------+-----------+---------------------------------------------------------------------------------------+------------------------------------------------+

