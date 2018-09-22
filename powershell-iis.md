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

```

get-item IIS:\AppPools\* | Select-Object -First 1 | Format-List -Property *