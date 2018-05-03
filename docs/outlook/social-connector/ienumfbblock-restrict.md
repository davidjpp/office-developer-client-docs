---
title: "IEnumFBBlockRestrict"
ms.author: soliver
author: soliver
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
localization_priority: Normal
ms.assetid: 887cea55-8f1c-45ec-3100-d03e1213d7c9
description: "Restricts the enumeration to a specified time period."
---

# IEnumFBBlock::Restrict

Restricts the enumeration to a specified time period.
  
## Quick Info

See [IEnumFBBlock](ienumfbblock.md).
  
```
HRESULT Restrict(  
    FILETIME ftmStart, 
    FILETIME ftmEnd 
);

```

## Parameters

 _ftmStart_
  
>  [in] The start time to restrict the enumeration. 
    
 _ftmEnd_
  
> [in] The end time to restrict the enumeration.
    
## Return Values

S_OK if the call succeeded; otherwise, an error code.
  
## Remarks

This method also resets the enumeration.
  
## See also

#### Concepts

[IEnumFBBlock::Clone](ienumfbblock-clone.md)
  
[IEnumFBBlock::Next](ienumfbblock-next.md)
  
[IEnumFBBlock::Reset](ienumfbblock-reset.md)
  
[IEnumFBBlock::Skip](ienumfbblock-skip.md)
  
[How to: Use relative time to access free/busy data](how-to-use-relative-time-to-access-free-busy-data.md)
