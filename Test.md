<div>
<img src="https://raw.githubusercontent.com/SASutherland/TechnicalWriter/master/Icon.PNG" align="left" vertical-align:"top">
<h1>Export the Transaction Store report</h1>
</div>
<p>
&nbsp
<p>

The **Transaction Store report** can be exported as a file. You can archive this file as a backup or print it off. For added redudancy, it is recommended to export the report during and after processing.

### Steps

1. Initiate the `tx_store_export` call based on the signature in the **tx_store_export_extern.h** file. Include the merchant account, terminal ID, and export format.

2. You should receive the formatted TxStore file. A receipt set is included with the report, which can be used for verification. 

```TypeScript
ADYLibraryResult result = tx_store_export(txexpReq, tx_store_export_CB, &POS);
```

### Allocate memory

Use `tx_store_export_allocate` to allocate memory for a `tx_store_export`. The library automatically frees this memory.  

### Parameters 

| Name | Type | Required | Description |
|:-----|:-----|:---------|-------------|
|`ped`| void | X | If not specified the PED object will be automatically populated. |
|`merchant_account`| char | ✓ | The merchant account processing this transaction. Transactions can be performed with any of the merchant accounts that were returned when registering the POS. Use a merchant account that you provided during [app registration](https://docs.adyen.com/point-of-sale/classic-library-integrations/com-extension-for-windows-integration/key-steps-com-extension/register-the-application-with-adyen-com-extension). |
|`terminal_id` | char | ✓ | The `terminal_id` of the PED. |
|`exportf` | export_format | ✓ | The format of the exported file. |
|`tender_reference` | char | X | The `tender_reference` of the transaction. |

### TxStoreReport Parameters

| Name | Type | Description |
|:-----|:-----|:------------|
|`tender_reference`| char | The `tender_reference` of the transaction.|
|`amount_currency`| char | The currency of the balance.  |
|`amount_value` | long | The value of the balance.|
|`timestamp`| char | Timestamp of the transaction. |
|`state`| ADYTenderState | 	Current state of the transaction. |
|`capture_pending`| int | Is set to "true" if a pending transaction exists on the PED, to be sent to the Adyen payments platform and captured. |
|`receipts`| [receipts_set](https://docs.adyen.com/point-of-sale/classic-library-integrations/c-library-integration/structs/receipt_set) | Set used to hold a list of receipt information. |
|`struct _tx_store_report * next` | struct | Struct that points to the next transaction in the set. |

### Code example

```TypeScript
typedef struct {
	//struct for passing any user data using echo_struct
  char *user_data;
} app_context_t;
 
//callback implementation
void tx_store_export_CB(tx_store_export_response *response, void *echo_struct) { 
	app_context_t * POS = (app_context_t *)echo_struct;
	//check the library result first to make sure it's successfully initialized
	if (response->parsed_result.library_result == ADYEN_LIBRARY_OK) {

		//print the export data
		printf("Export data:");
		if (response->exportf == export_format_humanreadable) {
			char * report = response->report.human;
			printf("Response is: %s", report);
		}

	} 
	else {
		printf("Data not available");
	}
}
 
main()
{
//Initialize library...
//Register application...
//Register device...

  app_context_t POS;
  //allocate
    tx_store_export_request *txexpReq = tx_store_export_allocate();
    //assign values
    txexpReq->merchant_account = strdup("Adyen");
    txexpReq->terminal_id = strdup("MX777-087098");
    txexpReq->exportf = export_format_humanreadable;
    txexpReq->tender_reference = strdup("986987987");
    //call export function
    ADYLibraryResult result = tx_store_export(txexpReq, tx_store_export_CB, &POS);

    sleep(10000); //sleep for 10 second to get the data in callback
}
```
