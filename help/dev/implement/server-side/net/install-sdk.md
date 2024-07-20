---
title: Instalar o SDK do .NET
description: Saiba como instalar o SDK do  [!DNL Adobe Target] .NET.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---

# Instalar o SDK do .NET

O SDK do .NET é distribuído por [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Para começar, adicione-a como uma dependência instalando via `Package Manage` ou `.NET CLI`:

## Gerenciador de pacotes

>[!BEGINTABS]

>[!TAB Gerenciador de pacotes]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>CLI [!TAB .NET]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

O código aberto pode ser encontrado em [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
