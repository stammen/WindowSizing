# WindowSizing
Set the size of a UWP window on first launch of a UWP app

UWP apps like to start up with a certain window size on first launch. The sample code demonstrates how to override this behavior.


The trick is to set the min window size before the window is activated. We do this is App.xaml.cs

```c#
using Windows.UI.ViewManagement;

protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    ApplicationView.PreferredLaunchViewSize = new Size(500, 800);
    ApplicationView.PreferredLaunchWindowingMode = ApplicationViewWindowingMode.PreferredLaunchViewSize;
    ApplicationView.GetForCurrentView().SetPreferredMinSize(new Size(500, 800));
```

Add an OnLoaded Handler in MainPage.xaml.cs

```c#
public MainPage()
{
    this.InitializeComponent();
    Loaded += OnLoaded;
}
```

In OnLoaded resize the window to your desired size 

```c#
using System.Diagnostics;
using Windows.UI.ViewManagement;

private void OnLoaded(object sender, RoutedEventArgs e)
{
    var result = ApplicationView.GetForCurrentView().TryResizeView(new Size(500, 800));
    Debug.WriteLine("OnLoaded TryResizeView: " + result);
}
```

