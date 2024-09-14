API
===

.. autosummary::
   :toctree: generated

### Get Price

.. http:get:: /api/get_price/

   Request for the best offer and obtain the necessary information of on-chain transaction

   :query string user_wallet_address: required
   :query string from_token_address: required
   :query string from_amount: required
   :query int slippage: required, 1 represent 1%

   **Example response**

   .. sourcecode:json
       {
            "status": 200,
            "results": {
               "query_order_id": "",
               "current_price": "",
               "expired_time": "",
               "price_source": "",               
               "min_return_amount":"",
               "jetton_receive_address": "",
               "send_ton_amount": "",
               "forward_ton_amount": "",
               "jetton_notify_opcode": ""
            }
       }

    .. note::

      The frontend needs to integrate ton-sdk and use the parameters returned by the Get Price API to construct on-chain transaction


### Get Order status

.. http:get:: /api/order_status/

   Use the query_order_id returned from the above request to check the current status of the transaction.

   :query string user_wallet_address: required
   :query string query_order_id: required


   **Example response**

   .. sourcecode:json
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