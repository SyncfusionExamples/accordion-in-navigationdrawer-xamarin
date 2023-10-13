# Accordion in NavigationDrawer in Xamarin.Forms
You can load the SfAccordion to the SfNavigationDrawer in Xamarin.Forms Accordion


Load the SfAccordion into the SfNavigationDrawer.DrawerContentView and bind the ViewModel property to the SfNavigationDrawer.IsOpen property to open the drawer. Add hamburger icon to the Image with Image.GestureRecognizer and bind the ViewModel command to the TapGestureRecognizer.Command to toggle the drawer.

**[XAML]**
```
<navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer" IsOpen="{Binding IsDrawerOpen, Mode=TwoWay}" DrawerHeaderHeight="160" DrawerFooterHeight="0" >
    <navigationdrawer:SfNavigationDrawer.ContentView>
        <Grid x:Name="mainContentView" BackgroundColor="White">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid BackgroundColor="#e8e8e8" >
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="50"/>
                    <ColumnDefinition Width="*"/>
                </Grid.ColumnDefinitions>
                <Image x:Name="hamburgerButton" Source="hamburger.png" HeightRequest="50" WidthRequest="40" Margin="5,0,0,0" HorizontalOptions="Start">
                    <Image.GestureRecognizers>
                        <TapGestureRecognizer Command="{Binding ToggleDrawerCommand}"/>
                    </Image.GestureRecognizers>
                </Image>
                <Label x:Name="headerLabel" Grid.Column="1" HeightRequest="50" HorizontalTextAlignment="Start" VerticalTextAlignment="Center" Text="Home" FontSize="16" TextColor="#385170" />
            </Grid>
            <Label Grid.Row="1" x:Name="contentLabel" VerticalOptions="Center" HorizontalOptions="Center" Text="Content View" FontSize="14"/>
        </Grid>
    </navigationdrawer:SfNavigationDrawer.ContentView>
    <navigationdrawer:SfNavigationDrawer.DrawerHeaderView>
        <Grid BackgroundColor="Black">
            <Image Source="Burger.jpg" HeightRequest="110" Margin="0,10,0,0" VerticalOptions="Center" HorizontalOptions="Center" Aspect="AspectFill"/>
        </Grid>
    </navigationdrawer:SfNavigationDrawer.DrawerHeaderView>
    <navigationdrawer:SfNavigationDrawer.DrawerContentView>
        <ContentView BackgroundColor="#323f4c">
            <ContentView.Content>
                <accordion:SfAccordion x:Name="accordion" BindableLayout.ItemsSource="{Binding Info}" ExpandMode="SingleOrNone" HeaderIconPosition="End">
                    <BindableLayout.ItemTemplate>
                        <DataTemplate>
                            <accordion:AccordionItem HeaderBackgroundColor="#1f2933" IconColor="#cbd2d9">
                                <accordion:AccordionItem.Header>
                                    <Grid>
                                        <Label Text="{Binding Name}" VerticalOptions="Center" HorizontalOptions="StartAndExpand" HeightRequest="50" TextColor="#cbd2d9" VerticalTextAlignment="Center"/>
                                    </Grid>
                                </accordion:AccordionItem.Header>
                                <accordion:AccordionItem.Content>
                                    <Grid Padding="5,0,0,0" BackgroundColor="#3e4c59">
                                        <Label Text="{Binding Description}" TextColor="#cbd2d9" VerticalOptions="Center"/>
                                    </Grid>
                                </accordion:AccordionItem.Content>
                            </accordion:AccordionItem>
                        </DataTemplate>
                    </BindableLayout.ItemTemplate>
                </accordion:SfAccordion>
            </ContentView.Content>
        </ContentView>
    </navigationdrawer:SfNavigationDrawer.DrawerContentView>
</navigationdrawer:SfNavigationDrawer>

```

**[C#]**

Change the IsOpen value in the command execution method to true.

```
public class ItemInfoRepository : INotifyPropertyChanged
{
    private bool isDrawerOpen;
 
    public Command ToggleDrawerCommand { get; set; }
 
    public bool IsDrawerOpen
    {
        get { return isDrawerOpen; }
        set
        {
            isDrawerOpen = value;
            this.OnPropertyChanged("IsDrawerOpen");
        }
    }
 
    public ItemInfoRepository()
    {
        ToggleDrawerCommand = new Command(OpenDrawer);
    }
 
    private void OpenDrawer(object obj)
    {
        IsDrawerOpen = true;
    }
}

```