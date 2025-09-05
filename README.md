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
Visual Studio 2017 or Visual Studio for Mac.
Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting
### Path too long exception
If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.