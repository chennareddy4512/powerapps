<properties
	pageTitle="Use Cognitive Services in PowerApps | Microsoft PowerApps"
	description="Build a basic app that uses the Microsoft Cognitive Services Text Analytics API to analyze text."
	services=""
	suite="powerapps"
	documentationCenter="na"
	authors="mgblythe"
	manager="anneta"
	editor=""
	tags=""/>

<tags
	ms.service="powerapps"
	ms.devlang="na"
	ms.topic="article"
	ms.tgt_pltfrm="na"
	ms.workload="na"
	ms.date="07/24/2017"
	ms.author="mblythe"/>

# Use Cognitive Services in PowerApps

This article shows you how to build a basic app that uses the [Microsoft Cognitive Services Text Analytics API](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview) to analyze text. We'll show you how to set up the Text Analytics API, and connect to it with the [Text Analytics connector](https://docs.microsoft.com/connectors/cognitiveservicestextanalytics/). Then we'll show you how to create an app that calls the API.

**Note**: If you are new to building apps in PowerApps, we recommend reading [Create an app from scratch](get-started-create-from-blank.md) before diving into this article.

## Introduction to Microsoft Cognitive Services

Microsoft Cognitive Services are a set of APIs, SDKs, and services available to make your applications more intelligent, engaging, and discoverable. These services enable you to easily add intelligent features – such as emotion and video detection; facial, speech and vision recognition; and speech and language understanding – into your applications.

We'll focus on "language understanding" for this article, working with the Text Analytics API. This API enables you to detect sentiment, key phrases, topics, and language from your text. Let's get started by trying out a demo of the API, then signing up for a preview version.

### Try out the Text Analytics API

The API has an online demo – you can see how it works, and look at the JSON that the service returns.

1. Go to the [Text Analytics API](https://azure.microsoft.com/services/cognitive-services/text-analytics/) page.

1. In the **See it in action** section, use the example text, or enter your own text. Then click or tap **Analyze**. 

    ![Text Analytics API demo](./media/cognitive-services-api/text-analytics-demo.png)

1. The page shows formatted results on the **Analyzed text** tab, and the JSON response on the **JSON** tab. [JSON](http://json.org/) is a way to represent data - in this case, data returned by the Text Analytics API.

## Sign up for the Text Analytics API

The API is available as a free preview, and it is associated with an Azure subscription. You manage the API through the Azure portal.

1. If you don't already have an Azure subscription, [sign up for a free subscription](https://azure.microsoft.com/free/).

1. Sign in to your Azure account.

1. Go to the [Create Cognitive Services blade](https://go.microsoft.com/fwlink/?LinkId=761108) in the Azure portal.

1. Enter information for the Text Analytics API, like in the following image. Select the **F0** (free) pricing tier.

    ![Create Text Analytics API](./media/cognitive-services-api/azure-create.png)

1. In the lower-left corner, click or tap **Create**.

1. On the **Dashboard**, click or tap the API that you just created.

    ![Azure dashboard](./media/cognitive-services-api/azure-dashboard.png)

1. Click or tap **Keys**.

    ![Azure menu](./media/cognitive-services-api/azure-menu-keys.png)

1. Copy one of the keys on the right of the screen. We will use this key later when we create a connection to the API.

    ![API keys](./media/cognitive-services-api/azure-keys.png)

## Build the app

Now that we have the Text Analytics API up and running, we can connect to it from PowerApps, and build an app that calls the API. This is a single screen app that provides functionality similar to the demo on the Text Analytics API page. Let's get started on building this!

### Create the app and add a connection

First, we'll create a blank phone app and add a connection with the **Text Analytics** connector. If you need more information about these tasks, see [Create an app from scratch](get-started-create-from-blank.md) and [Manage your connections in PowerApps](add-manage-connections.md).

1. In PowerApps Studio, click or tap **File** > **New**, then under **Blank app**, click or tap **Phone layout**.

    ![Blank app - phone layout](./media/cognitive-services-api/blank-app.png)

1. In the middle pane, click or tap **connect to data**.

1. In the right pane, click or tap **New connection** > **Text Analytics**.

    ![PowerApps data sources](./media/cognitive-services-api/data-sources.png)

1. Copy your key into **Account Key**, then click or tap **Create**.

    ![Text analytics connector](./media/cognitive-services-api/create-connection-ta.png)

### Add controls to the app

The next step in creating the app is to add all the controls. Normally when I build apps, I add formulas to the controls as I go, but in this case we'll focus on the controls first, then add a few formulas in the next section. The following image shows the app with all the controls.

![Finished app](./media/cognitive-services-api/finished-app-no-data.png)

Follow the steps below to create this screen. If a control name is specified, that name is used in a formula in the next section.

1. On the **Home** tab, click or tap **New Screen**, then **Scrollable screen**. 

1. On **Screen2**, select **[Title]** and change it to **Text Analysis**.

1. Add a **Label** control for the introductory text.

1. Add a **Text input** control, so we can enter text to analyze. Name the control **tiTextToAnalyze**. The app should now look like the following image.

    ![App with title, subtitle, and text input](./media/cognitive-services-api/partial-app-step1.png)

1. Add three **Check box** controls, so we can choose which API operations to perform. Name the controls **chkLanguage**, **chkPhrases**, and **chkSentiment**.

1. Add a button, so we can call the API after selecting which operations to perform. The app should now look like the following image.

    ![App with check boxes and button](./media/cognitive-services-api/partial-app-step2.png)

1. Add three **Label** controls. The first two will hold results from the language and sentiment API calls; the third is just an introduction for the gallery at the bottom of the screen.

1. Add a **Blank vertical gallery** control, then add a **Label** control to the gallery. The gallery will hold results from the key phrases API call. The app should now look like the following image.

    ![App with labels and gallery](./media/cognitive-services-api/partial-app-step3.png)

1. In the left pane, select **Screen1** > ellipsis (**. . .**) > **Delete** (we don't need this screen for our app).

We're keeping this app simple to focus on calling the Text Analytics API, but you could add things, like logic to show and hide controls based on the check boxes selected, error handling if the user doesn't select any options, and so on.

### Add logic to make the right API calls

OK, we have a nice-looking app, but it doesn't do anything yet. We'll fix that in a moment. But before we dive into the details, let's understand the pattern that the app follows:

1. The app makes specific API calls based on the check boxes selected in the app. When we click or tap **Analyze text**, the app makes 1, 2, or 3 API calls.

1. Data that the API returns is stored in three different [collections](working-with-variables.md#create-a-collection): **languageCollect**, **sentimentCollect**, and **phrasesCollect**.

1. The **Text** property for two of the labels, and the **Items** property for the gallery, are updated based on what's in the three collections.

With that background, let's add the formula for the **OnSelect** property of our button. This is where all the magic happens.

```
If(chkLanguage.Value=true,

        ClearCollect(languageCollect, TextAnalytics.DetectLanguage({numberOfLanguagesToDetect:1, text:tiTextToAnalyze.Text}).detectedLanguages.name)

);

If(chkPhrases.Value=true,

        ClearCollect(phrasesCollect, TextAnalytics.KeyPhrases({language:"en", text:tiTextToAnalyze.Text}).keyPhrases)

);

If(chkSentiment.Value=true,

        ClearCollect(sentimentCollect, TextAnalytics.DetectSentiment({language:"en", text:tiTextToAnalyze.Text}).score)

)
```

There's a bit going on here, so let's break it down:

- The **If** statements are straightforward – if a specific check box is selected, make the API call for that operation.
- Within each call, specify the appropriate parameters:
  - In all three calls, we specify **tiTextToAnalyze.Text** as the input text.
  - In **DetectLanguage()**, we hard-code **numberOfLanguagesToDetect** as 1, but we could pass this parameter based on some logic in the app.
  - In **KeyPhrases()** and **DetectSentiment()**, we hard-code language as "en", but we could pass this parameter based on some logic in the app. For example, we could detect the language first, then set this parameter based on what **DetectLanguage()** returns.
- For each call that is made, add the results to the appropriate collection:
  - For **languageCollect**, we add the **name** of the language that was identified in the text.
  - For **phrasesCollect**, we add the **keyPhrases** that were identified in the text.
  - For **sentimentCollect**, we add the sentiment **score** for the text, which is a value of 0-1, with 1 being 100% positive.


### Display the results of the API calls

To display the results of the API calls, reference the appropriate collection in each control:

1. Set the **Text** property of the language label to: `"The language detected is " & First(languageCollect).name`.

    The **First()** function returns the first (and in this case only) record in **languageCollect**, and we display the **name** (the only field) associated with that record.

1. Set the **Text** property of the sentiment label to: `"The sentiment score is " & Round(First(sentimentCollect.Value).Value, 3)\*100 & "% positive."`.

    This formula also uses the **First()** function, gets the **Value** (0-1) from the first and only record, then formats it as a percentage.

1. Set the **Items** property of the key phrases gallery to: `phrasesCollect`.

    We're now working with a gallery so we don't need the **First()** function to extract a single value. We reference the collection, and the gallery displays the key phrases as a list.

## Run the app

Now that the app is finished, let's run it to see how it works. In the following image, all three options are selected, and the text is the same as the default text on the Text Analytics API page.

![Finished app with data](./media/cognitive-services-api/finished-app.png)

If you compare the output of this app to the Text Analytics API page at the beginning of this article, you see that we get the same results.

We hope you now understand a little more about the Text Analytics API, and you've enjoyed seeing how to incorporate it into an app. Let us know if there are other Cognitive Services (or other services in general) that you would like us to focus on in our articles. As always, please leave feedback and any questions in the comments.