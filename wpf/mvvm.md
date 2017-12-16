# MVVM

1. [Recommendations and best practices for implementing MVVM and XAML/.NET applications](https://blog.rsuter.com/recommendations-best-practices-implementing-mvvm-xaml-net-applications/)  
Project file structure  
All MVVM/XAML applications should have a similar directory structure. The following tree shows a possible structure of a XAML application project:

* App.xaml
* Controls: Reusable UI controls (application independent views) without view models.
* Localization: Classes and resources for application localization
  * Strings.resx/.resw
* Models: Model and domain classes
* ViewModels: View models classes
  * MainWindowModel.cs
  * MyViewModel.cs
  * Dialogs
    * SelectItemDialogModel.cs
* Views: Contains the views
  * MainWindow.xaml
  * MyView.xaml
  * Dialogs
    * SelectItemDialog.xaml

2. [Devexpress MVVM 2013](https://community.devexpress.com/blogs/wpf/archive/2013/08/29/getting-started-with-devexpress-mvvm-framework-commands-and-view-models.aspx)