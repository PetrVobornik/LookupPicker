# <img src="https://github.com/PetrVobornik/LookupPicker/blob/master/images/lookuppicker-icon.png?raw=true" alt="LookupPicker" width="32" /> Lookup Picker for Xamarin.Forms 
The LookupPicker control extends the standard Picker control about the possibility to show of the names but storing (binding) of the keys. 
It brings two new properties: **ID** (bindable property which represents a key value of the selected item) and **ItemIdProperty** (name of the key property, e.g. "Id"). 
It is very useful for editing database data (e.g. by SQLite) with foreign key references, such as LookupComboBox in Delphi.

## NuGet
* Available on NuGet: https://www.nuget.org/packages/Amporis.Xamarin.Forms.LookupPicker [![NuGet](https://img.shields.io/nuget/v/Amporis.Xamarin.Forms.LookupPicker.svg?label=NuGet)](https://www.nuget.org/packages/Amporis.Xamarin.Forms.LookupPicker/)

## Instalation
Instal [NuGet](https://www.nuget.org/packages/Amporis.Xamarin.Forms.LookupPicker) or add a copy of the file [LookupPicker.cs](https://github.com/PetrVobornik/LookupPicker/blob/master/LookupPicker/LookupPicker.cs) into your Xamarin.Forms .NET Standard project (or to shared project). There is no need to add NuGet to platform specific projects.

## Usage

**Data classes**

```C#
public class Item
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int? TypeId { get; set; }
}

public class ItemType
{
    public int? IdType { get; set; }
    public string TypeName { get; set; }
}
```


**ItemDetial.xaml**

```xaml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:lp="clr-namespace:Amporis.Xamarin.Forms.LookupPicker"
             x:Class="LookupPickerSample.ItemDetial">
    <ContentPage.Content>
        <StackLayout>
            <Label Text="Name" />
            <Entry Text="{Binding Name}" Margin="0,2,0,10" />
            <Label Text="Type" />
            <lp:LookupPicker x:Name="lpType" Margin="0,2,0,10" 
                             ItemDisplayBinding="{Binding TypeName}" 
                             ItemIdProperty="IdType" ID="{Binding TypeId}" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```


**ItemDetial.xaml.cs**

```C#
public partial class ItemDetial : ContentPage
{
  protected async override void OnAppearing()
  {
    base.OnAppearing();
    BindingContext = new Item();
    lpType.ItemsSource = new [] {
      new ItemType() { IdType = null, TypeName = "" },    // optional first empty item
      new ItemType() { IdType = 1, TypeName = "Type 1" },
      new ItemType() { IdType = 2, TypeName = "Type 2" },
      new ItemType() { IdType = 3, TypeName = "Type 3" },
    };
  }
}
```

