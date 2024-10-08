---
title: Monitoring data reference for Azure Blob Storage
description: This article contains important reference material you need when you monitor Azure Blob Storage.
ms.date: 08/08/2024
ms.custom: horz-monitor
ms.topic: reference
author: normesta
ms.author: normesta
ms.service: azure-blob-storage
---

# Azure Blob Storage monitoring data reference

[!INCLUDE [horz-monitor-ref-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-intro.md)]

See [Monitor Azure Blob Storage](monitor-blob-storage.md) for details on the data you can collect for Azure Blob Storage and how to use it.

<a name="metrics-dimensions"></a>
[!INCLUDE [horz-monitor-ref-metrics-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-intro.md)]

### Supported metrics for Microsoft.Storage/storageAccounts
The following table lists the metrics available for the Microsoft.Storage/storageAccounts resource type.
[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]
[!INCLUDE [Microsoft.Storage/storageAccounts](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-storage-storageaccounts-metrics-include.md)]

### Supported metrics for Microsoft.Storage/storageAccounts/blobServices
The following table lists the metrics available for the Microsoft.Storage/storageAccounts/blobServices resource type.
[!INCLUDE [horz-monitor-ref-metrics-tableheader](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-tableheader.md)]
[!INCLUDE [Microsoft.Storage/storageAccounts/blobServices](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/metrics/microsoft-storage-storageaccounts-blobservices-metrics-include.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions-intro](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions-intro.md)]

[!INCLUDE [horz-monitor-ref-metrics-dimensions](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-metrics-dimensions.md)]

### Dimensions available to all storage services

[!INCLUDE [Metrics dimensions](../../../includes/azure-storage-account-metrics-dimensions.md)]

### Dimensions specific to Blob storage

| Dimension Name | Description |
| ------------------- | ----------------- |
| **BlobType** | The type of blob for Blob metrics only. The supported values are **BlockBlob**, **PageBlob**, and **Azure Data Lake Storage**. Append blobs are included in **BlockBlob**. |
| **Tier** | Azure storage offers different access tiers, which allow you to store blob object data in the most cost-effective manner. See more in [Azure Storage blob tier](../blobs/access-tiers-overview.md). The supported values include: <br><br>**Hot**: Hot tier<br>**Cool**: Cool tier<br>**Cold**: Cold tier<br>**Archive**: Archive tier<br>**Premium**: Premium tier for block blob<br>**P4/P6/P10/P15/P20/P30/P40/P50/P60**: Tier types for premium page blob<br>**Standard**: Tier type for standard page Blob<br>**Untiered**: Tier type for general purpose v1 storage account |

For the metrics supporting dimensions, you need to specify the dimension value to see the corresponding metrics values. For example, if you look at  **Transactions** value for successful responses, you need to filter the **ResponseType** dimension with **Success**. If you look at **BlobCount** value for Block Blob, you need to filter the **BlobType** dimension with **BlockBlob**.

<a name="resource-logs-preview"></a>
[!INCLUDE [horz-monitor-ref-resource-logs](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-resource-logs.md)]

### Supported resource logs for Microsoft.Storage/storageAccounts/blobServices
[!INCLUDE [Microsoft.Storage/storageAccounts/blobServices](~/reusable-content/ce-skilling/azure/includes/azure-monitor/reference/logs/microsoft-storage-storageaccounts-blobservices-logs-include.md)]

[!INCLUDE [horz-monitor-ref-logs-tables](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-logs-tables.md)]

- [AzureActivity](/azure/azure-monitor/reference/tables/azureactivity)
- [AzureMetrics](/azure/azure-monitor/reference/tables/azuremetrics)
- [StorageBlobLogs](/azure/azure-monitor/reference/tables/storagebloblogs)

The following sections describe the properties for Azure Storage resource logs when they're collected in Azure Monitor Logs or Azure Storage. The properties describe the operation, the service, and the type of authorization that was used to perform the operation.

### Fields that describe the operation

```json
{
    "time": "2019-02-28T19:10:21.2123117Z",
    "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/mytestrp/providers/Microsoft.Storage/storageAccounts/testaccount1/blobServices/default",
    "category": "StorageWrite",
    "operationName": "PutBlob",
    "operationVersion": "2017-04-17",
    "schemaVersion": "1.0",
    "statusCode": 201,
    "statusText": "Success",
    "durationMs": 5,
    "callerIpAddress": "192.168.0.1:11111",
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "location": "uswestcentral",
    "uri": "http://mystorageaccount.blob.core.windows.net/cont1/blobname?timeout=10"
}
```

[!INCLUDE [Account level capacity metrics](../../../includes/azure-storage-logs-properties-operation.md)]

### Fields that describe how the operation was authenticated

```json
{
    "identity": {
        "authorization": [
            {
                "action": "Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read",
                "denyAssignmentId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                "principals": [
                    {
                        "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                        "type": "User"
                    }
                ],
                "reason": "Policy",
                "result": "Granted",
                "roleAssignmentId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                "roleDefinitionId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
                "type": "RBAC"
            }
        ],
        "properties": {
            "metricResponseType": "Success",
            "objectKey": "/samplestorageaccount/samplecontainer/sampleblob.png"
           },
        "requester": {
            "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "audience": "https://storage.azure.com/",
            "objectId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "tokenIssuer": "https://sts.windows.net/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
           },
        "type": "OAuth"
    },
}

```

[!INCLUDE [Account level capacity metrics](../../../includes/azure-storage-logs-properties-authentication.md)]

### Fields that describe the service

```json
{
    "properties": {
        "accountName": "testaccount1",
        "requestUrl": "https://testaccount1.blob.core.windows.net:443/upload?restype=container&comp=list&prefix=&delimiter=/&marker=&maxresults=30&include=metadata&_=1551405598426",
        "userAgentHeader": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134",
        "referrerHeader": "blob:https://portal.azure.com/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "clientRequestId": "",
        "etag": "",
        "serverLatencyMs": 63,
        "serviceType": "blob",
        "operationCount": 0,
        "requestHeaderSize": 2658,
        "requestBodySize": 0,
        "responseHeaderSize": 295,
        "responseBodySize": 2018,
        "contentLengthHeader": 0,
        "requestMd5": "",
        "serverMd5": "",
        "lastModifiedTime": "",
        "conditionsUsed": "",
        "smbTreeConnectID" : "0x3",
        "smbPersistentHandleID" : "0x6003f",
        "smbVolatileHandleID" : "0xFFFFFFFF00000065",
        "smbMessageID" : "0x3b165",
        "smbCreditsConsumed" : "0x3",
        "smbCommandDetail" : "0x2000 bytes at offset 0xf2000",
        "smbFileId" : " 0x9223442405598953",
        "smbSessionID" : "0x8530280128000049",
        "smbCommandMajor" : "0x6",
        "smbCommandMinor" : "DirectoryCloseAndDelete"
    }
}
```

[!INCLUDE [Account level capacity metrics](../../../includes/azure-storage-logs-properties-service.md)]

[!INCLUDE [horz-monitor-ref-activity-log](~/reusable-content/ce-skilling/azure/includes/azure-monitor/horizontals/horz-monitor-ref-activity-log.md)]
- [Microsoft.Storage resource provider operations](/azure/role-based-access-control/resource-provider-operations#microsoftstorage)

## Related content

- See [Monitor Azure Blob Storage](monitor-blob-storage.md) for a description of monitoring Azure Blob Storage.
- See [Monitor Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.
