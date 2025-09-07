# conditional-navigation-treeview-xamarin
This repository demonstrates how to implement conditional navigation in a Syncfusion Xamarin.Forms TreeView. The sample shows how to navigate to different pages or perform specific actions based on which node the user selects in the TreeView. By applying conditions in the selection changed event or command, you can control navigation flow, restrict access, or trigger custom logic dynamically according to your application's requirements. 

## Sample

### XAML

Bind the SfTreeView.TapCommand to navigate to another page. By default, the TreeViewNode is the command parameter for the TapCommand.

```xaml
<syncfusion:SfTreeView x:Name="treeView" 
                    ChildPropertyName="SubFiles"
                    ItemTemplateContextType="Node"
                    AutoExpandMode="AllNodesExpanded"
                    ItemsSource="{Binding ImageNodeInfo}"
                    TapCommand="{Binding TreeViewTapCommand}">
    <syncfusion:SfTreeView.ItemTemplate>
        <DataTemplate>
            <Grid x:Name="grid" RowSpacing="0" >
                ...
            </Grid>
        </DataTemplate>
    </syncfusion:SfTreeView.ItemTemplate>
</syncfusion:SfTreeView>
```

### View Model

In the command execution method, skip the navigation for nodes based on TreeViewNode.Level.

```csharp
public class FileManagerViewModel
{
    public FileManagerViewModel()
    {
        TreeViewTapCommand = new Command<object>(OnTapped);
    }
 
    public Command<object> TreeViewTapCommand { get; set; }
 
    private void OnTapped(object obj)
    {
        var node = obj as Syncfusion.TreeView.Engine.TreeViewNode;
 
        if (node.Level == 0) return;
 
        var newPage = new Views.NewPage();
        newPage.BindingContext = node;
        App.Current.MainPage.Navigation.PushAsync(newPage);
    }
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for Xamarin](https://help.syncfusion.com/xamarin/system-requirements)

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
