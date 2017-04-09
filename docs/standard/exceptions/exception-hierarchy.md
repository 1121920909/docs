---
title: "Exception Hierarchy | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exceptions, types"
  - "runtime, exceptions"
  - "base exceptions"
  - "ApplicationException class"
  - "common language runtime, exceptions"
  - "COM interop, exceptions"
  - "exceptions, hierarchies"
ms.assetid: f7d68675-be06-40fb-a555-05f0c5a6f66b
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
---
# Exception Hierarchy
There are two types of exceptions: exceptions generated by an executing program, and exceptions generated by the common language runtime. In addition, there is a hierarchy of exceptions that can be thrown by either an application or the runtime.  
  
 The <xref:System.Exception?displayProperty=fullName> class        is the base class for exceptions. Several exception classes inherit directly from <xref:System.Exception>, including <xref:System.ApplicationException> and <xref:System.SystemException>. These two classes form the basis for almost all runtime exceptions.  
  
 Most exceptions that derive directly from <xref:System.Exception> add no functionality and no new members to it. For example, the <xref:System.InvalidCastException> class hierarchy is as follows:  
  
 <xref:System.Object> <xref:System.Exception> <xref:System.SystemException> <xref:System.InvalidCastException>  
  
 The runtime throws the appropriate derived class of <xref:System.SystemException> when errors occur. These errors result from failed runtime checks (such as array out-of-bound errors), and can occur during the execution of any method. If you are designing an application that creates new exceptions, you should derive those exceptions from the <xref:System.Exception> class. It is not recommended that you catch a <xref:System.SystemException>, nor is it good programming practice to throw a <xref:System.SystemException> in your application.  
  
 The most severe exceptions — those thrown by the runtime or in nonrecoverable conditions — include <xref:System.ExecutionEngineException>, <xref:System.StackOverflowException>, and <xref:System.OutOfMemoryException>.  
  
 Interoperation exceptions derive from <xref:System.SystemException> and are further extended by <xref:System.Runtime.InteropServices.ExternalException>. For example, <xref:System.Runtime.InteropServices.COMException> is the exception thrown during COM interop operations and derives from <xref:System.Runtime.InteropServices.ExternalException>. <xref:System.ComponentModel.Win32Exception> and <xref:System.Runtime.InteropServices.SEHException> also derive from <xref:System.Runtime.InteropServices.ExternalException>.  
  
## Hierarchy of Runtime Exceptions  
 The runtime has a base set of exceptions deriving from <xref:System.SystemException> that it throws when executing individual instructions. The following table hierarchically lists the standard exceptions provided by the runtime and the conditions under which you should create a derived class.  
  
|Exception type|Base type|Description|Example|  
|--------------------|---------------|-----------------|-------------|  
|[Exception](../../../docs/standard/exceptions/exception-class-and-properties.md)|<xref:System.Object>|Base class for all exceptions.|None (use a derived class of this exception).|  
|<xref:System.SystemException>|<xref:System.Exception>|Base class for all runtime-generated errors.|None (use a derived class of this exception).|  
|<xref:System.IndexOutOfRangeException>|<xref:System.SystemException>|Thrown by the runtime only when an array is indexed improperly.|Indexing an array outside its valid range:<br /><br /> `var i = arr[arr.Length + 1];`<br /><br /> `Dim i = arr(arr.Length + 1)`|  
|<xref:System.NullReferenceException>|<xref:System.SystemException>|Thrown by the runtime only when a null object is referenced.|`object o = null; string s = o.ToString();`<br /><br /> `Dim o As Object = Nothing Dim s As String = o.ToString()`|  
|<xref:System.AccessViolationException>|<xref:System.SystemException>|Thrown by the runtime only when invalid memory is accessed.|Occurs when interoperating with unmanaged code or unsafe managed code, and an invalid pointer is used.|  
|<xref:System.InvalidOperationException>|<xref:System.SystemException>|Thrown by methods when in an invalid state.|Calling the enumerator's `GetNext` method after removing an item from the underlying collection.|  
|<xref:System.ArgumentException>|<xref:System.SystemException>|Base class for all argument exceptions.|None (use a derived class of this exception).|  
|<xref:System.ArgumentNullException>|<xref:System.ArgumentException>|Thrown by methods that do not allow an argument to be null.|`String s = null; int i = "Calculate".IndexOf(s);`<br /><br /> `Dim s As String = Nothing Dim i As Integer = "Calculate".IndexOf(s)`|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.ArgumentException>|Thrown by methods that verify that arguments are in a given range.|`String s = "string"; s = s.Substring(s.Length + 1);`<br /><br /> `Dim s As String = "string" s = s.Substring(s.Length + 1)`|  
|<xref:System.Runtime.InteropServices.ExternalException>|<xref:System.SystemException>|Base class for exceptions that occur or are targeted at environments outside the runtime.|None (use a derived class of this exception).|  
|<xref:System.Runtime.InteropServices.COMException>|<xref:System.Runtime.InteropServices.ExternalException>|Exception encapsulating COM HRESULT information.|Used in COM interop.|  
|<xref:System.Runtime.InteropServices.SEHException>|<xref:System.Runtime.InteropServices.ExternalException>|Exception encapsulating Win32 structured exception handling information.|Used in unmanaged code interop.|  
  
## See Also  
 [Exception Class and Properties](../../../docs/standard/exceptions/exception-class-and-properties.md)   
 [Exception Handling Fundamentals](../../../docs/standard/exceptions/exception-handling-fundamentals.md)   
 [Best Practices for Exceptions](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [Exceptions](../../../docs/standard/exceptions/index.md)