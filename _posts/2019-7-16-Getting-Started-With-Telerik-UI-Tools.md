---
published: true
layout: post
title: Getting Started with Telerik UI for Xamarin - RadListView
date: 2019-07-16 12:23
comments: true
author: adamzucchi
tags: [Xamarin, Telerik]
---
Sorry for the super long delay in posts, I actually have quire a few drafts going but it's been way too long.  Anyways, I recently got back from Houston, TX after what was an **amazing** [Xamarin Developer Summit](https://xamarindevelopersummit.com) conference.  While at the conference I met tons of amazing people and companies, one of which was [Telerik](https://www.telerik.com) (a sponsor of the event).

I have always been interested in trying out new UI frameworks for Xamarin, more specificaly for Xamarin.Forms development.  I talked to the Telerik folks at their booth and got a demo of their tooling so I decided to give it a try.  Specifically I was very interested in their Xamarin.Forms ListView control called [RadListView](https://docs.telerik.com/devtools/xamarin/controls/listview/listview-overview).  Xamarin recently created a new ListView-esque control called CollectionView.  It looks promising however as of the writing of this article it is still in Preview and I try not to use Preview software in production apps.

### Telerik RadListView  
RadListView has what we developers have come to expect from ListView controls, virtualization, data binding, grouping, the ability to setup a DataTemplate for our ViewCell, etc. What's really nice is that it has a **SelectionMode** property where you can define whether or not you want to be able to select a **Single** item in the list, **Multiple** items in the list, or **None**.  Another awesome feature of RadListView is the ability to set different [layout definitions](https://docs.telerik.com/devtools/xamarin/controls/listview/listview-features-layouts).  The default layout is Linear Layout, but you can also use a Grid Layout (distributes your cells across a number of rows/columns).  Within each of these layouts is where you can also set an orientation for the RadListView, meaning your list can either scroll vertically (the default) or horizontally (which is not currently possible in the current Xamarin.Forms ListView).

### Getting Started  
I'll be honest getting started with Telerik proved to be challenging and very frustrating, however it may have been due in part to my previous Telerik account.  A couple of years ago I won a Telerik annual subscription through a great podcast called [.NET Rocks!](https://dotnetrocks.com).  This meant I already had a Telerik account associated with an email and I was unable to get the a new trial setup under this email.  Lucky for me I had access to the Telerik team at the conference and realized this pretty quickly and went and setup a new Telerik account under a new email that had never been associated with Telerik before.

Setting up this new email did not however mean I was off to the races :(  I unfortunately hit a roadblock where for some reason my computer (a Mac) was being served the Windows content (an .exe installer file).  This meant the Telerik team's user agent code was not properly working for all Macs.  Once again lucky for me, I had exchanged emails with the Telerik team at the conference and was able to work through these challenges.

1. Go to [Telerik's website](https://www.telerik.com/login/v2/telerik#register) and setup a new account (which you will use with your trial)
2. You will receive an email after creating your account, choose the 'verify' URL in the email
3. Download and install the [Telerik Xamarin UI Tools](https://www.telerik.com/download-trial-file/v2-b/ui-for-xamarin?file=pkg) - You may need to change the downloaded installer type based on your OS
4. Run and complete the installer
5. Open Visual Studio and create a new Xamarin.Forms app and update your Xamarin.Forms and Xamarin.Essentials Nuget packages so they are up-to-date.
6. Setting Up and Installing Telerik Nuget  
	1. Add the Telerik Nuget feed to Visual Studio with [this](https://nuget.telerik.com/nuget) URL and be sure to use the Telerik credentials you setup in step 1 above  
	2. In your new Xamarin.Forms solution open the Nuget package installer and set the source to the Telerik Nuget feed from the above step  
	3. Search for and install "Telerik.UI.for.Xamarin.Trial" into your projects - I tend to always install packages across all projects (.NET Standard project, iOS, Android, etc.)  
7. Take a look at my sample app on [Github](https://github.com/adamzucchi/TelerikUIToolsTest)

Since you are running the trial software you will be prompted with a couple of Telerik dialogs:
![alt text][monkeys]

8. I added the following Telerik namespaces:  

```  

xmlns:telerikDataControls="clr-namespace:Telerik.XamarinForms.DataControls;assembly=Telerik.XamarinForms.DataControls"  
xmlns:telerikListView="clr-namespace:Telerik.XamarinForms.DataControls.ListView;assembly=Telerik.XamarinForms.DataControls"  
xmlns:telerikListViewCommands="clr-namespace:Telerik.XamarinForms.DataControls.ListView.Commands;assembly=Telerik.XamarinForms.DataControls"  

```

9. Here is my RadListView XAML:

```  

<telerikDataControls:RadListView x:Name="listView" ItemsSource="{Binding People}" SelectionMode="Single" HorizontalOptions="FillAndExpand" VerticalOptions="FillAndExpand">
	<telerikDataControls:RadListView.Commands>
		<telerikListViewCommands:ListViewUserCommand Id="ItemTap" Command="{Binding ItemTapCommand}" />
	</telerikDataControls:RadListView.Commands>
	<telerikDataControls:RadListView.ItemTemplate>
		<DataTemplate>
			<telerikListView:ListViewTemplateCell>
				<telerikListView:ListViewTemplateCell.View>
					<Grid Padding="20"
						  HorizontalOptions="FillAndExpand"
						  VerticalOptions="Center">
						<Grid.RowDefinitions>
							<RowDefinition Height="Auto" />
							<RowDefinition Height="Auto" />
						</Grid.RowDefinitions>
						<Grid.ColumnDefinitions>
							<ColumnDefinition Width="75" />
							<ColumnDefinition Width="*" />
						</Grid.ColumnDefinitions>
						<Image Grid.Row="0" Grid.RowSpan="2" Grid.Column="0" WidthRequest="75" HeightRequest="75" Aspect="AspectFit" Source="{Binding Image}" VerticalOptions="Center" />
						<Label Grid.Row="0" Grid.Column="1" FontAttributes="Bold" Text="{Binding Name}" TextColor="Black" />
						<Label Grid.Row="1" Grid.Column="1" Text="{Binding Location}" TextColor="Black" />
					</Grid>
				</telerikListView:ListViewTemplateCell.View>
			</telerikListView:ListViewTemplateCell>
		</DataTemplate>
	</telerikDataControls:RadListView.ItemTemplate>
</telerikDataControls:RadListView>

```  

One thing to note about my XAML is that I am bound to a public ObservableCollection<Person> property called People, which the Person class has three properties, Image, Name, and Location.  If these names, locations, and images look familiar they should! These are from a sample app James Montemagno had previously put together that I tend to re-use : )

You may also notice the use of CoreMethods in my MainPageModel class. This is because I am using [FreshMvvm](https://github.com/rid00z/FreshMvvm)!  I am a **HUGE** fan of FreshMvvm and love to use it in both proof of concepts and production apps, not to mention Michael Ridland is an awesome guy!

### Result  
<video width="410" height="895" autoplay="true" controls>
	<source src="../images/20190716/monkeys.mp4" type="video/mp4" />
</video>

### Shortcomings and/or Bugs  
- Setup was initially painful, but with the help of the Telerik team I was able to get started so don't hesitate to contact them with questions - they are there to help!
- For some reason when I setup an ItemTap Command I am getting multiple commands to fire in a row for different rows in the list. This appears to depend on the length of the list (with shorter lists (3 items) I am not seeing this)

### The Good!  
- Support, support, support! Whenever I use code libraries or UI frameworks it is huge for my team and I to know we have support from the library creator/provider. This was definitely the case with Telerik and I cannot stress the importance of this enough.
-  Commands! Have the ability to wire up commands to your view/page model instead of event handlers in your view's code behind
- RadListView orientation support! Until CollectionView from Xamarin is out of Preview us developers need the ability to have horizontally scrolling virtualized lists
- Performance! From my demo and the SDKBrowser sample from Telerik performance seems to be amazing.

I hope to get in touch with Telerik in regards to the bug I came across with the ItemTap.  I'm guessing it is someothing super simple and probably on my end but I definitely plan to update this article once I have reached out and gotten a response. As always, thanks for reading!

[monkeys]:../images/20190716/monkeys.png "App Start"