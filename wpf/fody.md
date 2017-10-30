# Fody  
Extensible tool for weaving .net assemblies [Github](https://github.com/Fody/Fody)    

配置文件：```FodyWeavers.xml```

## PropertyChanged
### 添加 Nuget 包
``` bash
Install-Package PropertyChanged.Fody
```

### 编辑可选项  
1. EventInvokerNames  
Optional. Defaults to "OnPropertyChanged, NotifyOfPropertyChange, RaisePropertyChanged, NotifyPropertyChanged, NotifyChanged"
``` xml
<?xml version="1.0" encoding="utf-8" ?>
<Weavers>
  <PropertyChanged EventInvokerNames="NotifyPropertyChanged"/>
</Weavers>
```

2. InjectOnPropertyNameChanged  
Optional. Defaults to "true"  
``` xml
<?xml version="1.0" encoding="utf-8" ?>
<Weavers>
  <PropertyChanged InjectOnPropertyNameChanged='false'/>
</Weavers>
```

3. CheckForEquality  
Optional. Defaults to "true"
``` xml
<?xml version="1.0" encoding="utf-8" ?>
<Weavers>
  <PropertyChanged CheckForEquality='false'/>
</Weavers>
```

