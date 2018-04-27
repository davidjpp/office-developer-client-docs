---
title: "Connection Close Method, Table Type Property Example (VB)"
  
  
manager: soliver
ms.date: 11/16/2014
ms.audience: Developer
 
  
localization_priority: Normal
ms.assetid: cd0bb6ad-af7b-fb9c-d45c-5d4b62459c03
description: "Setting the ActiveConnection property to Nothing shouldclosethe catalog. Associated collections will be empty. Any objects that were created from schema objects in the catalog will be orphaned. Any properties on those objects that have been cached will still be available, but attempting to read properties that require a call to the provider will fail."
---

# Connection Close Method, Table Type Property Example (VB)

Setting the [ActiveConnection](activeconnection-property-adox.md) property to **Nothing** should "close" the catalog. Associated collections will be empty. Any objects that were created from schema objects in the catalog will be orphaned. Any properties on those objects that have been cached will still be available, but attempting to read properties that require a call to the provider will fail. 
  
```
 
' BeginCloseConnectionVB 
Sub Main() 
 On Error GoTo CloseConnectionByNothingError 
 
 Dim cnn As New ADODB.Connection 
 Dim cat As New ADOX.Catalog 
 Dim tbl As ADOX.Table 
 
 cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" &amp; _ 
 "Data Source= 'c:\Program Files\Microsoft Office\" &amp; _ 
 "Office\Samples\Northwind.mdb';" 
 Set cat.ActiveConnection = cnn 
 Set tbl = cat.Tables(0) 
 Debug.Print tbl.Type ' Cache tbl.Type info 
 Set cat.ActiveConnection = Nothing 
 Debug.Print tbl.Type ' tbl is orphaned 
 ' Previous line will succeed if this was cached 
 Debug.Print tbl.Columns(0).DefinedSize 
 ' Previous line will fail if this info has not been cached 
 
 'Clean up 
 cnn.Close 
 Set cat = Nothing 
 Set cnn = Nothing 
 Exit Sub 
 
CloseConnectionByNothingError: 
 Set cat = Nothing 
 
 If Not cnn Is Nothing Then 
 If cnn.State = adStateOpen Then cnn.Close 
 End If 
 Set cnn = Nothing 
 
 If Err <> 0 Then 
 MsgBox Err.Source &amp; "-->" &amp; Err.Description, , "Error" 
 End If 
End Sub 
' EndCloseConnectionVB 

```

Closing a [Connection](connection-object-ado.md) object that was used to "open" the catalog should have the same effect as setting the **ActiveConnection** property to **Nothing**. 
  
```
Sub CloseConnection() 
 On Error GoTo CloseConnectionError 
 
 Dim cnn As New ADODB.Connection 
 Dim cat As New ADOX.Catalog 
 Dim tbl As ADOX.Table 
 
 cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" &amp; _ 
 "Data Source= 'c:\Program Files\Microsoft Office\" &amp; _ 
 "Office\Samples\Northwind.mdb';" 
 Set cat.ActiveConnection = cnn 
 Set tbl = cat.Tables(0) 
 Debug.Print tbl.Type ' Cache tbl.Type info 
 cnn.Close 
 Debug.Print tbl.Type ' tbl is orphaned 
 ' Previous line will succeed if this was cached 
 Debug.Print tbl.Columns(0).DefinedSize 
 ' Previous line will fail if this info has not been cached 
 
 'Clean up 
 Set cat = Nothing 
 Set cnn = Nothing 
 Exit Sub 
 
CloseConnectionError: 
 
 Set cat = Nothing 
 
 If Not cnn Is Nothing Then 
 If cnn.State = adStateOpen Then cnn.Close 
 End If 
 Set cnn = Nothing 
 
 If Err <> 0 Then 
 MsgBox Err.Source &amp; "-->" &amp; Err.Description, , "Error" 
 End If 
End Sub 
' EndCloseConnection2VB 

```

