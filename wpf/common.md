# WPF 需知

## 设计时

[mc:Ignorable Attribute](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/mc-ignorable-attribute)
``` xml
<object  
  xmlns:ignorablePrefix1="ignorableUri"  
  xmlns:ignorablePrefix2="ignorableUri2"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix1 ignorablePrefix2"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/> 
</object>
```

使用ViewModelLocator 模式开发时，设计时无法预览 ViewModel 中的数据效果。
```xml
mc:Ignorable="d"
d:DataContext="{d:DesignInstance Type=vm:MainWindowViewModel, IsDesignTimeCreatable=True}"
```

