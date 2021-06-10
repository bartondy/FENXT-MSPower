# FENXT-MSPower

SETUP REQUIREMENTS

1.	Confirm access to an FENXT environment with ability to access APPLICATIONS in the FENXT Control Panel
      •	It will be necessary to add an “application” to the FENXT instance, which will connect the custom Power Platform connector to that specific instance
      
2.	Configure access to MS Power Automate with login
      •	A version of Microsoft (Office) 365 that includes MS Power Platform is required
      •	FENXTCustom Connector will be accessible through Power Automate (Flow) and Power Apps
      •	Go to https://us.flow.microsoft.com/ and confirm the ability to login
     
     
     
     
STEPS TO CONFIGURE (SUMMARY)

 - Create New Application at BB Developer Site

 - Configure FENXT Connector in MS Power Platform




CREATE NEW APPLICATION AT BLACKBAUD DEVELOPER SITE

1.	Go to https://developer.blackbaud.com/apps/ and ensure Blackbaud profile is signed in

2.	Click to add a new app, fill in information.  

3.	Enter organization name and Website.  If internal or for testing, any information can be entered.

4.	Once saved, notice the application ID and application secret.  Those will be needed when creating the custom connector.  You can get back to these values at any time by going to https://developer.blackbaud.com/apps/ and opening the application you just created.


![image](https://user-images.githubusercontent.com/70080319/121523030-c1abce80-c9c3-11eb-9859-f1629b4a924e.png)


5.	In the Redirect URIs section, click Edit, Add a redirect URI and then paste:  https://global.consent.azure-apim.net/redirect 

6.	Go to the instance of FENXT that will be integrated.  Click Control Panel, Applications

7.	Click Connect app, paste the Application ID referenced in Step 4

8.	That completes the configuration within Blackbaud… now on to the Connector



