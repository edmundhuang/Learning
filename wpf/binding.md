# 数据绑定

1. 绑定到其它元素
``` xml
<Grid>
    <StackPanel>
        <TextBox x:Name="textbox1" />
        <Label Content="{Binding ElementName=textbox1, Path=Text}" />
    </StackPanel>
</Grid>
```

2. 绑定到静态资源
``` xml
<Window.Resources>
        <ContentControl x:Key="text">Hello, World!</ContentControl>
</Window.Resources>
<Grid>
    <StackPanel>
        <Label x:Name="label1" Content="{Binding Source={StaticResource text}}" />
    </StackPanel>
</Grid>
```

3. 绑定到自身
``` xml
<Grid>
    <StackPanel>
        <Label x:Name="label1" Content="{Binding RelativeSource={RelativeSource Self}, Path=Name}" />
    </StackPanel>
</Grid>
```

4. 绑定到指定类型的父元素
``` xml
<Grid x:Name="Grid1">
        <StackPanel>
            <Label x:Name="label1" Content="{Binding RelativeSource={RelativeSource FindAncestor, 
                AncestorType={x:Type Grid}}, Path=Name}" />
        </StackPanel>
</Grid>
```

5. 绑定到对象 
``` cs
public class Perscs
    public string Name { get; set;cs
    public int Age { get; set; } 
}
```

``` xml
<StackPanel x:Name="stackPanel"> 
        <StackPanel.DataContext> 
            <local:Person Name="Jack" Age="30"></local:Person> 
        </StackPanel.DataContext> 
        <TextBlock  Text="{Binding Path=Name}"></TextBlock> 
        <TextBlock Text="{Binding Path=Age}"></TextBlock>        
</StackPanel>
```

6. 绑定到集合
``` cs
public class Person 
{ 
        public string Name { get; set; } 
        public int Age { get; set; } 
}

public class PersonList : ObservableCollection<Person> 
{ }
```

``` xml
<Window.Resources> 
    <local:PersonList x:Key="person"> 
        <local:Person Name="Jack" Age="30"></local:Person> 
        <local:Person Name="Tom" Age="32"></local:Person> 
    </local:PersonList> 
</Window.Resources> 
<StackPanel x:Name="stackPanel"> 
    <ListBox  ItemsSource="{Binding Source={StaticResource ResourceKey=person}}" 
               DisplayMemberPath="Name">            
    </ListBox> 
</StackPanel>
```

7. DataContext共享源  
我们需要将同一资源绑定到多个 UI 元素上，很显然到处写 "{Binding Source={StaticResource person}}" 是件很繁琐且不利于修改的做法。WPF 提供了一个称之为 "数据上下文 (DataContext)" 的东西让我们可以在多个元素上共享一个源对象，只需将其放到父元素 DataContext 属性即可。当我们不给 Binding 扩展标志指定 Source 属性时，它会自动寻找上级父元素的数据上下文。

``` xml
<Window.Resources> 
    <local:PersonList x:Key="person"> 
        <local:Person Name="Jack" Age="30"></local:Person> 
        <local:Person Name="Tom" Age="32"></local:Person> 
    </local:PersonList> 
</Window.Resources> 
<StackPanel x:Name="stackPanel" DataContext="{StaticResource person}"> 
    <ListBox  ItemsSource="{Binding}" 
               DisplayMemberPath="Name">            
    </ListBox> 
</StackPanel>
```

8. 使用XML作为Binding的源  
``` xml
<?xml version="1.0" encoding="utf-8" ?> 
<PersonList> 
  <Person Id="1"> 
    <Name>Jack</Name> 
  </Person> 
  <Person Id="2"> 
    <Name>Tom</Name> 
  </Person> 
  <Person Id="3"> 
    <Name>Justin</Name> 
  </Person> 
  <Person Id="4"> 
    <Name>David</Name> 
  </Person> 
</PersonList>
```

``` xml
<StackPanel> 
    <ListView x:Name="personListView"> 
        <ListView.View> 
            <GridView> 
                <GridViewColumn Header="Id" Width="100" 
                                 DisplayMemberBinding="{Binding XPath=@Id}"/> 
                <GridViewColumn Header="Name" Width="100" 
                                 DisplayMemberBinding="{Binding XPath=Name}"/> 
            </GridView> 
        </ListView.View> 
    </ListView>    
    <Button Click="Button_Click">Load Data</Button> 
</StackPanel>
```

``` cs
private void Button_Click(object sender, RoutedEventArgs e) 
{ 
    XmlDocument xmlDocument = new XmlDocument(); 
    xmlDocument.Load("Person.xml");

    XmlDataProvider xdp = new XmlDataProvider(); 
    xdp.Document = xmlDocument; 
    xdp.XPath = @"/PersonList/Person";

    this.personListView.DataContext = xdp; 
    this.personListView.SetBinding(ListView.ItemsSourceProperty, new Binding()); 
}
```

