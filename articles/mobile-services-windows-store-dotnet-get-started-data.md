<properties 
	pageTitle="Add Mobile Services to an existing app (Windows Store) | Mobile Dev Center" 
	description="Learn how to get started using Mobile Services to leverage data in your Windows Store app." 
	services="mobile-services" 
	documentationCenter="windows" 
	authors="ggailey777" 
	manager="dwrede" 
	editor=""/>

<tags 
	ms.service="mobile-services" 
	ms.workload="mobile" 
	ms.tgt_pltfrm="" 
	ms.devlang="dotnet" 
	ms.topic="article" 
	ms.date="09/19/2014" 
	ms.author="glenga"/>

# Get started with data in Mobile Services

[AZURE.INCLUDE [mobile-services-selector-get-started-data-legacy](../includes/mobile-services-selector-get-started-data-legacy.md)]


<div class="dev-center-tutorial-subselector">
	<a href="/en-us/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-get-started-data/" title=".NET backend">.NET backend</a> | 
	<a href="/en-us/documentation/articles/mobile-services-windows-store-dotnet-get-started-data/" title="JavaScript backend" class="current">JavaScript backend</a>
</div>


This topic shows you how to use Azure Mobile Services to leverage data in a Windows Store app. In this tutorial, you will download a Visual Studio 2013 project for an app that stores data in memory, create a new mobile service, integrate the mobile service with the app, and then sign-in to the Azure Management Portal to view changes to data made when running the app.

>[AZURE.NOTE]This topic shows you how to use Visual Studio 2013 to add Azure Mobile Services to a Windows Store project. You can add the same JavaScript backend mobile service to a universal Windows app project. For more information, see the [universal Windows app version](/en-us/documentation/articles/mobile-services-javascript-backend-windows-universal-dotnet-get-started-data) of this tutorial. 

This tutorial walks you through these basic steps:

1. [Download the Windows Store app project][Get the Windows Store app] 
2. [Create the mobile service from Visual Studio]
3. [Add a data table for storage]
4. [Update the app to use the mobile service]
5. [Test the app against Mobile Services]

To complete this tutorial, you need the following:

* An active Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see [Azure Free Trial](http://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-services-windows-store-dotnet-get-started-data%2F).
* Visual Studio 2013, which makes it easier to connect your Windows Store app to Mobile Services. 

##<a name="download-app"></a>Download the GetStartedWithData project

This tutorial is built on the [GetStartedWithMobileServices app][Developer Code Samples site], which is a Windows Store app project in Visual Studio 2013. The UI for this app is identical to the app generated by the Mobile Services quickstart, except that added items are stored locally in memory. 

1. Download the C# version of the GetStartedWithMobileServices sample app from the [Developer Code Samples site]. 

2. In Visual Studio 2013, open the downloaded project and examine the MainPage.xaml.cs file.

   	Notice that added **TodoItem** objects are stored in an in-memory **ObservableCollection&lt;TodoItem&gt;**.

3. Press the **F5** key to rebuild the project and start the app.

4. In the app, type some text in **Insert a TodoItem**, then click **Save**.

   	![][0]  

   	Notice that the saved text is displayed in the second column under **Query and update data**.

##<a name="create-service"></a>Create a new mobile service from Visual Studio

[AZURE.INCLUDE [mobile-services-create-new-service-vs2013](../includes/mobile-services-create-new-service-vs2013.md)]

<ol start="7"><li><p>In Solution Explorer, open the App.xaml.cs code file, and notice the new static field that was added to the **App** class, which looks like the following example:</p> 

		<pre><code>public static Microsoft.WindowsAzure.MobileServices.MobileServiceClient 
		    todolistClient = new Microsoft.WindowsAzure.MobileServices.MobileServiceClient(
		        "https://todolist.azure-mobile.net/",
		        "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX");
		</code></pre>

	<p>This code provides access to your new mobile service in your app by using an instance of the <a href="http://go.microsoft.com/fwlink/p/?LinkId=302030">MobileServiceClient class</a>. The client is created by supplying the URI and the application key of the new mobile service. This static field is available to all pages in your app.</p>
</li>
</ol>

##<a name="add-table"></a>Add a new table for data storage

[AZURE.INCLUDE [mobile-services-create-new-table-vs2013](../includes/mobile-services-create-new-table-vs2013.md)]

>[AZURE.NOTE]New tables are created with the Id, __createdAt, __updatedAt, and __version columns. When dynamic schema is enabled, Mobile Services automatically generates new columns based on the JSON object in the insert or update request. For more information, see [Dynamic schema](http://msdn.microsoft.com/en-us/library/windowsazure/jj193175.aspx).

#<a name="update-app"></a>Update the app to use the mobile service

[AZURE.INCLUDE [mobile-services-windows-dotnet-update-data-app](../includes/mobile-services-windows-dotnet-update-data-app.md)]

##<a name="test-app"></a>Test the app against your new mobile service

1. In Visual Studio, press the F5 key to run the app.

2. As before, type text in **Insert a TodoItem**, and then click **Save**.

   	This sends a new item as an insert to the mobile service.

3. In the [Management Portal], click **Mobile Services**, and then click your mobile service.

4. Click the **Data** tab, then click **Browse**.

   	![][9]
  
   	Notice that the **TodoItem** table now contains data, with id values generated by Mobile Services, and that columns have been automatically added to the table to match the TodoItem class in the app.

5. In the app, check one of the items in the list, then go back to the Browse tab in the portal and click **Refresh**. 

  	Notice that the complete value has changed from **false** to **true**.

6. In the MainPage.xaml.cs project file, replace the existing **RefreshTodoItems** method with the following code that filters out completed items:

        private async void RefreshTodoItems()
        {                       
            // This query filters out completed TodoItems. 
            items = await todoTable
               .Where(todoItem => todoItem.Complete == false)
               .ToCollectionAsync();

            ListItems.ItemsSource = items;            
        }

7. In the app, check another one of the items in the list and then click the **Refresh** button.

   	Notice that the checked item now disappears from the list. Each refresh results in a round-trip to the mobile service, which now returns filtered data.

This concludes the **Get started with data** tutorial.

## <a name="next-steps"> </a>Next steps

This tutorial demonstrated the basics of enabling a Windows Store app to work with data in Mobile Services. Next, consider completing one of the following tutorials that is based on the GetStartedWithData app that you created in this tutorial:

* [Validate and modify data with scripts]
  <br/>Learn more about using server scripts in Mobile Services to validate and change data sent from your app.

* [Refine queries with paging]
  <br/>Learn how to use paging in queries to control the amount of data handled in a single request.

Once you have completed the data series, try one of these other tutorials:

* [Get started with authentication]
  <br/>Learn how to authenticate users of your app.

* [Get started with push notifications] 
  <br/>Learn how to send a very basic push notification to your app.

* [Mobile Services .NET How-to Conceptual Reference]
  <br/>Learn more about how to use Mobile Services with .NET.
  
<!-- Anchors. -->

[Get the Windows Store app]: #download-app
[Create the mobile service from Visual Studio]: #create-service
[Add a data table for storage]: #add-table
[Update the app to use the mobile service]: #update-app
[Test the app against Mobile Services]: #test-app
[Next Steps]:#next-steps

<!-- Images. -->
[0]: ./media/mobile-services-windows-store-dotnet-get-started-data-vs2013/mobile-quickstart-startup.png

[9]: ./media/mobile-services-windows-store-dotnet-get-started-data-vs2013/mobile-todoitem-data-browse.png
[10]: ./media/mobile-services-windows-store-dotnet-get-started-data-vs2013/mobile-data-sample-download-dotnet-vs12.png


<!-- URLs. -->
[Validate and modify data with scripts]: /en-us/documentation/articles/mobile-services-windows-store-dotnet-validate-modify-data-server-scripts/
[Refine queries with paging]: /en-us/documentation/articles/mobile-services-windows-store-dotnet-add-paging-data/
[Get started with Mobile Services]: /en-us/documentation/articles/mobile-services-javascript-backend-windows-store-dotnet-get-started/
[Get started with data]: /en-us/documentation/articles/mobile-services-windows-store-dotnet-get-started-data/
[Get started with authentication]: /en-us/documentation/articles/mobile-services-windows-store-dotnet-get-started-users/
[Get started with push notifications]: /en-us/documentation/articles/mobile-services-javascript-backend-windows-store-dotnet-get-started-push/
[Mobile Services .NET How-to Conceptual Reference]: /en-us/documentation/articles/mobile-services-windows-dotnet-how-to-use-client-library/

[Azure Management Portal]: https://manage.windowsazure.com/
[Management Portal]: https://manage.windowsazure.com/
[Mobile Services SDK]: http://go.microsoft.com/fwlink/p/?LinkId=257545
[Developer Code Samples site]:  http://go.microsoft.com/fwlink/p/?LinkId=328660

[MobileServiceClient class]: http://go.microsoft.com/fwlink/p/?LinkId=302030
