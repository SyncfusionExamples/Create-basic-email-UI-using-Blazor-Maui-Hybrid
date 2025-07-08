# Create-basic-email-UI-using-Blazor-Maui-Hybrid
This repository contains a sample explaining how to create basic email UI using Blazor Maui Hybrid.

## Creating Your First Blazor Hybrid App
### Getting Started: Create a New .NET MAUI Project
Creating your first Blazor Hybrid app with .NET MAUI is a straightforward process. Follow these steps to get started:
* Open Visual Studio on your computer.
* In the start menu, click on “Create a new project.”
* In the project templates list, find and select ".NET MAUI Blazor Hybrid App."
* Enter a name for your project. Choose a folder location where the project files will be saved.
* Confirm your project setup. Choose the appropriate .NET framework version, either .NET 8.0 or .NET 9.0, depending on your target framework requirements.

### Adding a Blazor RichTextEditor
* Open NuGet Package Manager in Visual Studio.
* Search for "Syncfusion.Blazor.RichTextEditor" and install it.

### Registering Syncfusion Blazor Service
1.	Add the Syncfusion Namespace: Open the /Imports.razor file in your project. Add the Syncfusion.Blazor namespace to ensure your application knows where to find the components:
Imports.razor
@using Syncfusion.Blazor

2.	Register the Syncfusion Service: Open the MauiProgram.cs file. Register the Syncfusion service so it integrates with your MAUI and Blazor app:

**MauiProgram.cs**

```
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        . . .
        builder.Services.AddSyncfusionBlazor();
        . . .
    }
}
```

### Adding Stylesheet and script References
To ensure that your RichTextEditor and other Syncfusion components render correctly, it's crucial to add the necessary style sheet and script references to your project. Here's how you can do this using Static Web Assets in the <head> section of your wwwroot/index.html file:

**index.html**
```
<head>
. . .
    <link href="_content/Syncfusion.Blazor.Themes/bootstrap5.css" rel="stylesheet" />
    <script src="_content/Syncfusion.Blazor.Core/scripts/syncfusion-blazor.min.js" type="text/javascript" />
. . .
</head>
```

>Note: 
Check out the Blazor Themes topic to discover various methods (Static Web Assets, CDN, and CRG) for referencing themes in your Blazor application. Also, check out the Adding Script Reference topic to learn different approaches for adding script references in your Blazor application.

### Integrating the RichTextEditor
To integrate the RichTextEditor component into your application, you can embed it within any Razor file, such as Home.razor. Here's how you can do it:
* Add the Syncfusion Namespace to Your Razor File: First, ensure you have the necessary namespace for Syncfusion included in your Razor file. This is essential for using the RichTextEditor component.
* Embed the RichTextEditor Component: Within the Razor file, you can now add the RichTextEditor component to facilitate rich text input. Here is a simple example of embedding it in Home.razor:

**Home.razor**
```
@using Syncfusion.Blazor.RichTextEditor

<SfRichTextEditor>
    <p>Rich Text Editor allows to insert images from online source as well as local computer where you want to insert the image in your content.</p>
    <p><b>Get started Quick Toolbar to click on the image</b></p>
    <p>It is possible to add custom style on the selected image inside the Rich Text Editor through quick toolbar.</p>
...
</SfRichTextEditor>
```

### Build and run the application
To launch the RichTextEditor component, build and run the project.
 
If you want the RichTextEditor to display alone on your output screen, you'll need to modify your MainLayout.razor file. Simply remove any sidebar and top row elements that are currently there. This will ensure that the RichTextEditor takes up the full display area, providing a focused user experience.
 

## Combining Blazor and MAUI Components: 
To create a basic email UI using MAUI's AutoComplete feature alongside the Blazor RichTextEditor, you'll need to follow these steps:
1.	Install the Syncfusion.Maui.Inputs NuGet Package: Begin by installing the Syncfusion.Maui.Inputs NuGet package. This package is necessary to utilize MAUI's AutoComplete feature as part of your email user interface.
2.	Register the Handler in MauiProgram.cs: Next, you'll need to register the handler for the Syncfusion Maui core within your MauiProgram.cs file. This is essential for setting up the components correctly.

**MauiProgram.cs**
```
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        . . .
        builder.ConfigureSyncfusionCore();
        . . .
    }
}
```

3.	Implement MAUI AutoComplete in MainPage.Xaml: You will use the MAUI AutoComplete component to manage inputs for fields like 'To', 'Cc', 'Bcc', and 'Subject'. 
4.	Use the Blazor RichTextEditor for the Email Body: For the email body, use the Blazor RichTextEditor component, which you can integrate into your Blazor WebView element. 
Here's an example of how you can set this up in MainPage.xaml:

**MainPage.xaml**
```
<ContentPage 
...
             xmlns:inputs="clr-namespace:Syncfusion.Maui.Inputs;assembly=Syncfusion.Maui.Inputs"
             x:Class="BlazorMauiHybridApp.MainPage">

    <Grid RowDefinitions="50,50,50,50,50,Auto">

        <Grid ColumnDefinitions="Auto,*,Auto" Background="Navy" Grid.Row="0">
            <Label Text="Email-Compose" TextColor="White" FontAttributes="Bold" HorizontalOptions="Start" VerticalOptions="Center" Margin="5"/>
            <HorizontalStackLayout Grid.Column="2" HorizontalOptions="End" VerticalOptions="Center">
                <Label Text="ATTACH" TextColor="White" FontAttributes="Bold" Margin="5"/>
                <Label Text="SEND" TextColor="White" FontAttributes="Bold" Margin="5"/>
            </HorizontalStackLayout>
        </Grid>

        <Grid ColumnDefinitions="40, *" Grid.Row="1">
            <Label Text="To" TextColor="Gray" Margin="5" VerticalOptions="Center"/>
            <inputs:SfAutocomplete Grid.Column="1" Margin="5" VerticalOptions="Center"/>
        </Grid>

        <Grid ColumnDefinitions="40, *" Grid.Row="2">
            <Label Text="Cc" TextColor="Gray" Margin="5" VerticalOptions="Center"/>
            <inputs:SfAutocomplete Grid.Column="1" Margin="5" VerticalOptions="Center"/>
        </Grid>

        <Grid ColumnDefinitions="40, *" Grid.Row="3">
            <Label Text="Bcc" TextColor="Gray" Margin="5" VerticalOptions="Center"/>
            <inputs:SfAutocomplete Grid.Column="1" Margin="5" VerticalOptions="Center"/>
        </Grid>

        <inputs:SfAutocomplete Grid.Row="4" Placeholder="Subject" Margin="5" VerticalOptions="Center"/>

        <BlazorWebView x:Name="blazorWebView" Grid.Row="5" HeightRequest="300" HostPage="wwwroot/index.html">
            <BlazorWebView.RootComponents>
                <RootComponent Selector="#app" ComponentType="{x:Type local:Components.Routes}" />
            </BlazorWebView.RootComponents>
        </BlazorWebView>

    </Grid>

</ContentPage>
```
