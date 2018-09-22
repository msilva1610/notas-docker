## Alterando application pool com  powershell

### Caso necessário importar o módulo web administration

```
Import-Module WebAdministration 
```

### Listando os Applications Pools

```
Get-Item IIS:\AppPools\* 
```

### Listando os aplication pool e selecionando o primeiro item

```
get-item IIS:\AppPools\* | Select-Object -First 1
```
Resultado:

```
Name                     State        Applications
----                     -----        ------------
.NET v4.5                Started
PSDrive                     : IIS
PSProvider                  : WebAdministration
```

### Listando as propriedades no formato lista

```
get-item IIS:\AppPools\* | Select-Object -First 1 | Format-List -Property *
```

Resultado:

```
Attributes                  : {name, queueLength, autoStart, enable32BitAppOnWin64...}
name                        : .NET v4.5odel, recycling, failure, cpu...}
queueLength                 : 1000
autoStart                   : Truert, Stop, Recycle}
enable32BitAppOnWin64       : Falsesoft.IIs.PowerShell.Framework.ConfigurationElementSchema
managedRuntimeVersion       : v4.0
managedRuntimeLoader        : webengine4.dll
enableConfigurationOverride : True
managedPipelineMode         : Integrated
CLRConfigFile               :
passAnonymousToken          : True
startMode                   : OnDemand
state                       : Started
applicationPoolSid          : S-1-5-82-271721585-897601226-2024613209-625570482-296978595
processModel                : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
recycling                   : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
failure                     : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
cpu                         : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
environmentVariables        : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
workerProcesses             : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
ItemXPath                   : /system.applicationHost/applicationPools/add[@name='.NET v4.5']
PSPath                      : WebAdministration::\\51DA722991C3\AppPools\.NET v4.5
PSParentPath                : WebAdministration::\\51DA722991C3\AppPools
PSChildName                 : .NET v4.5
PSDrive                     : IIS
PSProvider                  : WebAdministration
PSIsContainer               : True
Attributes                  : {name, queueLength, autoStart, enable32BitAppOnWin64...}
ChildElements               : {processModel, recycling, failure, cpu...}
ElementTagName              : add
Methods                     : {Start, Stop, Recycle}
Schema                      : Microsoft.IIs.PowerShell.Framework.ConfigurationElementSchema
```

### Listando um especifico application pool

```
get-item IIS:\AppPools\DefaultAppPool
```

Resultado:

```
Name                     State        Applications
----                     -----        ------------
DefaultAppPool           Started      icareclientes
```

### Listando um especifico application pool e suas propriedades

```
get-item IIS:\AppPools\DefaultAppPool | Format-List -Property *
```

Resultado:

```
name                        : DefaultAppPool
queueLength                 : 1000
autoStart                   : True
enable32BitAppOnWin64       : False
managedRuntimeVersion       : v4.0
managedRuntimeLoader        : webengine4.dll
enableConfigurationOverride : True
managedPipelineMode         : Integrated
CLRConfigFile               :
passAnonymousToken          : True
startMode                   : OnDemand
state                       : Started
applicationPoolSid          : S-1-5-82-3006700770-424185619-1745488364-794895919-4004696415
processModel                : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
recycling                   : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
failure                     : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
cpu                         : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
environmentVariables        : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
workerProcesses             : Microsoft.IIs.PowerShell.Framework.ConfigurationElement
ItemXPath                   : /system.applicationHost/applicationPools/add[@name='DefaultAppPool']
PSPath                      : WebAdministration::\\51DA722991C3\AppPools\DefaultAppPool
PSParentPath                : WebAdministration::\\51DA722991C3\AppPools
PSChildName                 : DefaultAppPool
PSDrive                     : IIS
PSProvider                  : WebAdministration
PSIsContainer               : True
Attributes                  : {name, queueLength, autoStart, enable32BitAppOnWin64...}
ChildElements               : {processModel, recycling, failure, cpu...}
ElementTagName              : add
Methods                     : {Start, Stop, Recycle}
Schema                      : Microsoft.IIs.PowerShell.Framework.ConfigurationElementSchema
```

Pode especificar a propriedade

```
get-item IIS:\AppPools\DefaultAppPool | Format-List -Property PSDrive
```

### Analisar as propriedades detalhadas de um ChildElement

```
get-item IIS:\AppPools\DefaultAppPool | Get-ItemProperty -name processModel
```

Resultado:

```
identityType           : LocalService
userName               :
password               :
loadUserProfile        : False
setProfileEnvironment  : True
logonType              : LogonBatch
manualGroupMembership  : False
idleTimeout            : 00:20:00
idleTimeoutAction      : Terminate
maxProcesses           : 1
shutdownTimeLimit      : 00:01:30
startupTimeLimit       : 00:01:30
pingingEnabled         : True
pingInterval           : 00:00:30
pingResponseTime       : 00:01:30
logEventOnProcessModel : IdleTimeout
PSPath                 : WebAdministration::\\51DA722991C3\AppPools\DefaultAppPool
PSParentPath           : WebAdministration::\\51DA722991C3\AppPools
PSChildName            : DefaultAppPool
PSProvider             : WebAdministration
Attributes             : {identityType, userName, password, loadUserProfile...}
ChildElements          : {}
ElementTagName         : processModel
Methods                :
Schema                 : Microsoft.IIs.PowerShell.Framework.ConfigurationElementSchema
```

### Outra forma deescrever o mesmo comando

```
(get-item IIS:\AppPools\DefaultAppPool).processModel
```

ou utilizando o get-ItemProperty

```
Get-ItemProperty IIS:\AppPools\DefaultAppPool -name processModel
```

## Alterando os valores das propriedades

Observar que as propriedades são case sensitive. Os valores apenas serão alterados se forem escritos corretamentes

```
Set-ItemProperty IIS:\AppPools\DefaultAppPool -name processModel.identityType -value 'LocalService'
```

ou utilizar o id da propriedade

```
Set-ItemProperty IIS:\AppPools\DefaultAppPool -name processModel.identityType -value 1
```