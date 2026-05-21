---
title: Instalar o .NET SDK
description: Saiba como instalar o SDK  [!DNL Adobe Target] .NET.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
TQID: https://experienceleague.adobe.com/438ax3dEUclYIa42EvOLyBBuRngsZLHRDXabumxp0F8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 63
ht-degree: 9%

---

# Instalar o .NET SDK

O .NET SDK é distribuído por [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Para começar, adicione-a como uma dependência instalando via `Package Manage` ou `.NET CLI`:

## Gerenciador de pacotes

>[!BEGINTABS]

>[!TAB Gerenciador de pacotes]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB CLI  .NET]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

O código aberto pode ser encontrado em [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
