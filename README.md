# LookupPicker
LookupPicker extends a standard Picker control for possibility to show of names but storing (binding) of keys. 
It brings two new properties: ID (bindable property which represents key value of the selected item) and ItemIdProperty (name of the key property, e.g. "Id").
It is very useful for editing database (e.g. SQLite) data with foreign key references.

## Instalation
Add a copy of the file LookupPicker.cs into your project (common part). You can also change the namespace in this file.

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
    public int? TypeId { get; set; }
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
                             ItemIdProperty="TypeId" ID="{Binding TypeId}" />
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
      new ItemType() { TypeId = null, TypeName = "" },    // optional first empty item
      new ItemType() { TypeId = 1, TypeName = "Type 1" },
      new ItemType() { TypeId = 2, TypeName = "Type 2" },
      new ItemType() { TypeId = 3, TypeName = "Type 3" },
    };
  }
}
```

