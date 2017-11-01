# mahapps.metro

## 安装
```bash
Install-Package MahApps.Metro  ### 正式版
### 或者
Install-Package MahApps.Metro -Pre  ### 预览版
```

## Metro 风格的窗口
MainWindow.xaml
```xml
<Controls:MetroWindow x:Class="WpfApplication.MainWindow"
                      xmlns:Controls="http://metro.mahapps.com/winfx/xaml/controls"
                      >

  <!-- your content -->

</Controls:MetroWindow>
```

修改 MainWindow.xaml.cs
``` cs
public partial class MainWindow  // 去除从Window继承，则使用XAML中定义的MetroWindow，此处使用MetroWindow继承也可以。
{
  public MainWindow()
  {
    InitializeComponent();
  }
}
```

## 内置样式
App.xaml
```xml
<Application x:Class="WpfApplication.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
  <Application.Resources>
    <ResourceDictionary>
      <ResourceDictionary.MergedDictionaries>
        <!-- MahApps.Metro resource dictionaries. Make sure that all file names are Case Sensitive! -->
        <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Controls.xaml" />
        <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Fonts.xaml" />
        <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Colors.xaml" />
        <!-- Accent and AppTheme setting -->
        <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Accents/Blue.xaml" />
        <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Accents/BaseLight.xaml" />
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </Application.Resources>
</Application>
```

## 资源包
``` bash
Install-Package MahApps.Metro.Resources
```


