# Building Your Interface
There is no set way to design and build your interface however, there are some standards that you must follow in order to successfully submit requests.

## Domain Restrictions
To avoid abuse of your access rights by third party sites, each customer is provided a secure endpoint that will only respond to requests from a specific domain. Prior to creating your endpoint, you will need to provide Geo-Connections details with regard to the domain through which you will be submitting requests.

Additionally, if you would like to allow third party sites to make requests against your end point (for example a manufacturer providing an interface to distributors) the best implementation is to embed the interface in an iframe. This allows the third party to appear to submit the form directly without taking on the additional cost of creating a separate end point for each third party site.

## API Key
All customers are provided a unique api key which must be included in the request header as 'x-api-key'.

### jQuery Ajax Example:

```js

	$("#gse_form").submit(function(e){
		var postData = $(this).serializeArray();
		var formURL = $(this).attr("action");
		$.ajax(
		{
			url : formURL,
			type: "POST",
			data : postData,
			crossDomain:true,
			headers:{'x-api-key':'YOUR API KEY HERE'},
			success:function(data, textStatus, jqXHR){
				// Handle Response
				},
			error: function(jqXHR, textStatus, errorThrown){
				// Handle Errored Request
				}
		});
		e.preventDefault(); //STOP default action
		e.unbind; //unbind. to stop multiple form submit.
	});
	
```

## Form Labels
The Name defined in the Inputs section of this documentation must be used as the 'name' attribute for the form input element to successfully submit the contents of your form.

## Attribution
LoopLink<sup>&reg;</sup> GSE uses a variety geo-coding services to perform location searches. All of these service providers deserve and require credit for their work. If provided in the reponse your interface must display attribution details to the end user in the results section.

Failure to properly credit these service providers can result in their refusal to provide their services to us. As such, we will revoke access rights to any endpoint that is not properly crediting these services.

## Additional Guidance
If during the design of your interface you have any questions or problems, please do not hesitate to call Geo-Connections&reg; at 866-995-4449.