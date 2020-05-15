---
title: GetSharedEntities Service Operation - Campaign Management
ms.service: bing-ads-campaign-management-service
ms.topic: article
author: eric-urban
ms.author: eur
description: Gets negative keyword lists or website exclusion lists.
dev_langs: 
  - csharp
  - java
  - php
  - python
---
# GetSharedEntities Service Operation - Campaign Management
Gets negative keyword lists or website exclusion lists. 

> [!TIP] 
> For an overview, see the [Negative Keywords](../guides/negative-keywords.md) and [Negative Sites](../guides/negative-sites.md) technical guides. 

> [!IMPORTANT]
> Only the users of the manager account (customer) that owns a website exclusion list ([PlacementExclusionList](placementexclusionlist.md)) can update or delete the list, add or delete list items, and associate the list with ad accounts. If your ad account is associated with a website exclusion list that you do not own, you can disassociate the list from your account, but the list and list items are read-only. The owner of the list is determined by the association's [SharedEntityCustomerId](sharedentityassociation.md#sharedentitycustomerid) element.
> 
> If you have access to multiple manager accounts in an account hierarchy, the operation's results can vary depending on the CustomerId [request header](#request-header) element that you set. 

## <a name="request"></a>Request Elements
The *GetSharedEntitiesRequest* object defines the [body](#request-body) and [header](#request-header) elements of the service operation request. The elements must be in the same order as shown in the [Request SOAP](#request-soap). 

> [!NOTE]
> Unless otherwise noted below, all request elements are required.

### <a name="request-body"></a>Request Body Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="sharedentityscope"></a>SharedEntityScope|Indicates whether the shared entity is available at the ad account ([Account](entityscope.md#account)) or manager account ([Customer](entityscope.md#customer)) level.<br/><br/>This element is optional and defaults to [Account](entityscope.md#account) scope. The ad account scope is only applicable for negative keyword lists.<br/><br/>Set this element to [Customer](entityscope.md#customer) to get website exclusion lists in your manager account (customer) shared library.|[EntityScope](entityscope.md)|
|<a name="sharedentitytype"></a>SharedEntityType|The type of shared entity to get from the ad account or manager account (customer) library.<br/><br/>Set this element to NegativeKeywordList to get negative keyword lists ([NegativeKeywordList](negativekeywordlist.md)) in your ad account shared library.<br/><br/>Set this element to PlacementExclusionList to get website exclusion lists ([PlacementExclusionList](placementexclusionlist.md)) in your manager account (customer) shared library.|**string**|

### <a name="request-header"></a>Request Header Elements
[!INCLUDE[request-header](./includes/request-header.md)]

## <a name="response"></a>Response Elements
The *GetSharedEntitiesResponse* object defines the [body](#response-body) and [header](#response-header) elements of the service operation response. The elements are returned in the same order as shown in the [Response SOAP](#response-soap).

### <a name="response-body"></a>Response Body Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="sharedentities"></a>SharedEntities|The negative keyword lists or website exclusion lists.|[SharedEntity](sharedentity.md) array|

### <a name="response-header"></a>Response Header Elements
[!INCLUDE[response-header](./includes/response-header.md)]

## <a name="request-soap"></a>Request SOAP
This template was generated by a tool to show the [order](../guides/services-protocol.md#element-order) of the [body](#request-body) and [header](#request-header) elements for the SOAP request. For supported types that you can use with this service operation, see the [Request Body Elements](#request-body) reference above.

```xml
<s:Envelope xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Header xmlns="https://bingads.microsoft.com/CampaignManagement/v13">
    <Action mustUnderstand="1">GetSharedEntities</Action>
    <AuthenticationToken i:nil="false">ValueHere</AuthenticationToken>
    <CustomerAccountId i:nil="false">ValueHere</CustomerAccountId>
    <CustomerId i:nil="false">ValueHere</CustomerId>
    <DeveloperToken i:nil="false">ValueHere</DeveloperToken>
  </s:Header>
  <s:Body>
    <GetSharedEntitiesRequest xmlns="https://bingads.microsoft.com/CampaignManagement/v13">
      <SharedEntityType i:nil="false">ValueHere</SharedEntityType>
      <SharedEntityScope i:nil="false">ValueHere</SharedEntityScope>
    </GetSharedEntitiesRequest>
  </s:Body>
</s:Envelope>
```

## <a name="response-soap"></a>Response SOAP
This template was generated by a tool to show the order of the [body](#response-body) and [header](#response-header) elements for the SOAP response.

```xml
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Header xmlns="https://bingads.microsoft.com/CampaignManagement/v13">
    <TrackingId d3p1:nil="false" xmlns:d3p1="http://www.w3.org/2001/XMLSchema-instance">ValueHere</TrackingId>
  </s:Header>
  <s:Body>
    <GetSharedEntitiesResponse xmlns="https://bingads.microsoft.com/CampaignManagement/v13">
      <SharedEntities d4p1:nil="false" xmlns:d4p1="http://www.w3.org/2001/XMLSchema-instance">
        <SharedEntity d4p1:type="-- derived type specified here with the appropriate prefix --">
          <AssociationCount d4p1:nil="false">ValueHere</AssociationCount>
          <ForwardCompatibilityMap xmlns:e323="http://schemas.datacontract.org/2004/07/System.Collections.Generic" d4p1:nil="false">
            <e323:KeyValuePairOfstringstring>
              <e323:key d4p1:nil="false">ValueHere</e323:key>
              <e323:value d4p1:nil="false">ValueHere</e323:value>
            </e323:KeyValuePairOfstringstring>
          </ForwardCompatibilityMap>
          <Id d4p1:nil="false">ValueHere</Id>
          <Name d4p1:nil="false">ValueHere</Name>
          <Type d4p1:nil="false">ValueHere</Type>
          <!--This field is applicable if the derived type attribute is set to SharedList-->
          <ItemCount d4p1:nil="false">ValueHere</ItemCount>
        </SharedEntity>
      </SharedEntities>
    </GetSharedEntitiesResponse>
  </s:Body>
</s:Envelope>
```

## <a name="example"></a>Code Syntax
The example syntax can be used with [Bing Ads SDKs](../guides/client-libraries.md). See [Bing Ads API Code Examples](../guides/code-examples.md) for more examples.
```csharp
public async Task<GetSharedEntitiesResponse> GetSharedEntitiesAsync(
	string sharedEntityType,
	EntityScope? sharedEntityScope)
{
	var request = new GetSharedEntitiesRequest
	{
		SharedEntityType = sharedEntityType,
		SharedEntityScope = sharedEntityScope
	};

	return (await CampaignManagementService.CallAsync((s, r) => s.GetSharedEntitiesAsync(r), request));
}
```
```java
static GetSharedEntitiesResponse getSharedEntities(
	java.lang.String sharedEntityType,
	EntityScope sharedEntityScope) throws RemoteException, Exception
{
	GetSharedEntitiesRequest request = new GetSharedEntitiesRequest();

	request.setSharedEntityType(sharedEntityType);
	request.setSharedEntityScope(sharedEntityScope);

	return CampaignManagementService.getService().getSharedEntities(request);
}
```
```php
static function GetSharedEntities(
	$sharedEntityType,
	$sharedEntityScope)
{

	$GLOBALS['Proxy'] = $GLOBALS['CampaignManagementProxy'];

	$request = new GetSharedEntitiesRequest();

	$request->SharedEntityType = $sharedEntityType;
	$request->SharedEntityScope = $sharedEntityScope;

	return $GLOBALS['CampaignManagementProxy']->GetService()->GetSharedEntities($request);
}
```
```python
response=campaignmanagement_service.GetSharedEntities(
	SharedEntityType=SharedEntityType,
	SharedEntityScope=SharedEntityScope)
```

## Requirements
Service: [CampaignManagementService.svc v13](https://campaign.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/v13/CampaignManagementService.svc)  
Namespace: https\://bingads.microsoft.com/CampaignManagement/v13  
