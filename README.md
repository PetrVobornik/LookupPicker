
# LookupPicker
LookupPicker extends a standard Picker control for possibility to show of names but storing (binding) of keys. 
It brings two new properties: ID (bindable property which represents key value of the selected item) and ItemIdProperty (name of the key property, e.g. "Id").
It is very useful for editing database (e.g. SQLite) data with foreign key references.

## Instalation
Add a copy of the file LookupPicker.cs into your project (common part). You can also change the namespace in this file.

## Usage

<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:lp="clr-namespace:Amporis.Xamarin.Forms.LookupPicker"
             x:Class="LookupPickerSample.ItemDetial"
             Title="Pacient">
    <ContentPage.Content>
        <StackLayout Margin="20">
            <Label Text="Name" />
            <Entry Text="{Binding Name}" Margin="0,2,0,10" />
            <Label Text="Type" />
            <lp:LookupPicker x:Name="lpType" Margin="0,2,0,10" 
                             ItemDisplayBinding="{Binding TypeName}" ItemIdProperty="Id"
                             ID="{Binding TypeId}"/>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
