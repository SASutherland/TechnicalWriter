<div>
<img src="https://raw.githubusercontent.com/SASutherland/TechnicalWriter/master/Icon.PNG" align="left" vertical-align:"top">
<h1>Export the Transaction Store report</h1>
</div>
<p>
&nbsp
<p>

The **Transaction Store report** can be exported as a file. You can archive this file as a backup or print it off. For additional redudancy, it is recommended to export the Transaction Store report during and after processing. To do so, follow these steps:

1. Send a `tx_store_export` request. Be sure to include the account, terminal ID, and export format. Memory is automatically allocated for the request.
2. You should receive a `tx_store_export_reponse` with the formatted Transaction Store report. A receipt set is included with the report and can be used for verification. 

---

### Method

| Name | Description |
| :--- | :---------- |
|`tx_store_export` | Used to export the `TxStoreReport` file. | 

### Parameters

| Name | Type | Description |
|:------|:-----|:------------|
|`tender_reference`| char | The `tender_reference` of the transaction.|
|`amount_currency`| char | The currency of the balance.  |
|`amount_value` | long | The value of the balance.|
|`timestamp`| char | Timestamp of the transaction. |
|`state`| ADYTenderState | 	Current state of the transaction. |
|`capture_pending`| int | Is set to "true" if a pending transaction exists on the PED, to be sent to the Adyen payments platform and captured. |
|`receipts`| [receipts_set](https://docs.adyen.com/point-of-sale/classic-library-integrations/c-library-integration/structs/receipt_set) | Set used to hold a list of receipt information. |
