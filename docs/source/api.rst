API
===

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 2


Quote
--------------------------------

.. http:get:: /quote

   Request for the best offer and obtain the necessary information of on-chain transaction

   :query string chainId: required (ton:1100)
   :query string fromTokenAddress: required
   :query string toTokenAddress: required
   :query string fromAmount: required
   :query string userAddr: required
   :query int slippage: required, 1 represent 1%

   **Example response**

   .. sourcecode:: json

       {
            "quoteId": 0,                    //unique id
            "resAmount": "string",           //return toToken amount
            "minReturnAmount": "string",     //return minimum toToken amount
            "data": "string",                //if ton chain, use as jetton_notify_opcode
            "to": "string",                  //if ton chain, use as jetton_receive_address
            "fee": "string",                 
            "feeRate": 0,
            "targetDecimals": 0,              
            "reFreshTime": 0,                //quote refresh time, unix timestamp (half of deadLine)
            "deadLine": 0,                   //excute expire time, unix timestamp
            "price": "string",               //fromTokenPrice / toTokenPrice
            "gasAmount": "string",
            "tonForwardGasAmount": "string"
       }


Submit Order
--------------------------------

.. http:post:: /submit-order

   After the frontend send the transaction, submit the order information to the backend

   :query int quoteId: required
   :query string userAddr: required
   :query string hash: required

   **Example response**

   .. sourcecode:: json

       {
            "orderId": 0                    //unique id
       }



Get Order status
--------------------------------

.. http:get:: /order

   Use the quoteId returned from the above request to check the current status of the transaction.

   :query string quoteId: required
   :query string orderId: required

   **Example response**

   .. sourcecode:: json

       {
            "timestamp": 0,                  //order record time
            "fromAmount": "string",
            "quoteId": 0,
            "quotePrice": "string",
            "quoteSlippage": 0,
            "fromHash": "string",
            "toHash": "string",
            "fromToken": "string",
            "toToken": "string",
            "fromTokenSymbol": "string",
            "toTokenSymbol": "string",
            "fromTokenDecimals": 0,
            "toTokenDecimals": 0,
            "fromTokenLogo": "string",
            "toTokenLogo": "string",
            "side": 0,                       //0-buy, 1-sell
            "fillPrice": "string",
            "fillAmount": "string",
            "payAmount": "string",
            "status": 0                      //1-pending 2-success 3-failed
       }


Get Order List
--------------------------------

.. http:get:: /order/list

   :query string chainId: required (ton:1100)
   :query string userAddr: required
   :query int page: optional
   :query int size: optional

   **Example response**

   .. sourcecode:: json

       {
            "status": 200,
            "results": {
               "order_status": "", // 0 pending, 1 done, 2 revert
               "from_token_address": "",
               "to_token_address": "",
               "from_amount": "",
               "return_amount": "",
               "settle_source": ""
            }
       }

       {
            "total": 0,
            "currentPage": 0,
            "maxPage": 0,
            "list": [
               {
                  "timestamp": 0,
                  "fromAmount": "string",
                  "quoteId": 0,
                  "quotePrice": "string",
                  "quoteSlippage": 0,
                  "fromHash": "string",
                  "toHash": "string",
                  "fromToken": "string",
                  "toToken": "string",
                  "fromTokenSymbol": "string",
                  "toTokenSymbol": "string",
                  "fromTokenDecimals": 0,
                  "toTokenDecimals": 0,
                  "fromTokenLogo": "string",
                  "toTokenLogo": "string",
                  "side": 0,
                  "fillPrice": "string",
                  "fillAmount": "string",
                  "payAmount": "string",
                  "status": 0
               }
            ]
       }  

