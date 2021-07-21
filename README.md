# Blackbaud Financial Edge NXT® Custom Connector for Microsoft Power Platform

The code and instructions provided in this repository by [npAutomate](https://npautomate.com/) can be used to create a custom connector for Blackbaud Financial Edge NXT to Microsoft Power Platform.

## Prerequisites

1. Confirm access to Blackbaud Financial Edge NXT® solution.
2. As an environment administrator, ability to connect applications from the [Blackbaud Marketplace Manage](https://app.blackbaud.com/marketplace/manage) page.
It will be necessary to manually sideload an *application* to the Blackbaud environment that contains Financial Edge NXT. This makes sure you'll be able to connect the custom Power Platform connector to your specific Blackbaud environment.
3. Confirm login access to Microsoft Power Automate. 
      - A version of Microsoft (Office) 365 that includes Microsoft Power Platform is required.
      - Financial Edge NXT® Custom Connector will be accessible through Power Automate (Flow) and Power Apps.
      - Go to [Micorosoft Power Automate](https://us.flow.microsoft.com) and confirm the ability to login.


## Create a new application with Blackbaud SKY Developer Portal

1. If you do not already have one, sign up for a [Blackbaud SKY Developer account](https://developer.blackbaud.com/signup). This account represents you as a "developer" within the Blackbaud Developer Portal and enables you to create applications. If you don't already have a Blackbaud ID, it will also prompt you to create one. 
If you do have one, sign in to your Blackbaud account.
2. Go to Blackbaud SKY Developer [My applications page](https://developer.blackbaud.com/apps/) and select **Add**.
3. Fill out the Add application screen. We recommend you name it something that helps you identify it as your Financial Edge NXT® custom connector.
4. Once saved, take note of the **application ID** and **application secret**.  Those are needed when you create the custom connector.  You can get back to these values at any time by going to the Blackbaud SKY Developer [My applications page](https://developer.blackbaud.com/apps/) and opening the application you created.

![image](https://user-images.githubusercontent.com/70080319/121523030-c1abce80-c9c3-11eb-9859-f1629b4a924e.png)

5. Under **Redirect URIs**, select **Edit**. Then, add this as your redirect URI:  https://global.consent.azure-apim.net/redirect 
6. Go to the [Blackbaud Marketplace Manage](https://app.blackbaud.com/marketplace/manage) page.
7. Select **Connect**. Paste in your **application ID** as referenced in Step 4.

This completes the configuration portion with Blackbaud. Now you are ready to configure the connector. 

## Configure the Financial Edge NXT® custom connector

1. Download the [**FENXT-Power-Connector.swagger.json**](https://github.com/bartondy/FENXT-MSPower/blob/main/FENXT-Power-Connector.swagger.json) file from this Github repo.
2. Log in to [Microsoft Power Automate](https://flow.microsoft.com).
3. On the left menu, select **Data**, **Custom connectors**. 
4. Select **New Custom Connector**, **Import an OpenAPI file**.
6. Assign a connector name, such as "FENXT Automate Connector."
7. Select **Import** and choose the **FENXT-Power-Connector.swagger.json** file on your computer that you downloaded in step one, and then select **Open**.
8. Go to the **Security** tab.  Ensure OAuth 2.0 is selected.  Enter the client ID (Application ID) and client secret (application secret) from the [Blackbaud Developer app](https://developer.blackbaud.com/apps/) that was created.
9. Update **Refresh URL** to mirror the token URL:  https://oauth2.sky.blackbaud.com/token.

![image](https://user-images.githubusercontent.com/70080319/121524943-d0938080-c9c5-11eb-8bbb-286b43700da7.png)

8. At the top, select **Create connector**, then go to the **Definition** page.
9. On the Definition page, first define a **Policy** to allow for Oauth 2 authentication to a specific Financial Edge NXT® environment.  Scroll down and select **New Policy**.

      1. **Name**:  Enter something like “FE Conn”
      2. **Template**:  Set HTTP Header
      3. **Operations**:  Leave blank
      4. **Header name**:  `Bb-Api-Subscription-Key`
      5. **Header Value**:  Enter the primary access key or secondary access key defined from the Blackbaud SKY Developer Portal [My subscriptions]( https://developer.blackbaud.com/subscriptions/). If you don't have a subscription, susbcribe to the **Standard APIs**.
      6. **Action if header exists**:  override
      7. **Run policy on**:  Request  
      
![image](https://user-images.githubusercontent.com/70080319/121525301-29fbaf80-c9c6-11eb-8d48-a4fab869a3c2.png)

10. Select **Update Connector**.
11. Test the connection using a standard `GET` for account or project.  If successful, the connected Financial Edge NXT® database is accessible from Power Automate and Power Apps.
12. Congratulations, the Financial Edge NXT® custom connector is accessible from the **Custom** section within the **Add an Action** function of Power Automate.

![image](https://user-images.githubusercontent.com/70080319/121526061-09802500-c9c7-11eb-8651-746e77f0d0c8.png)





