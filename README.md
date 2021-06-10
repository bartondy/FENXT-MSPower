# FENXT-MSPower

SETUP REQUIREMENTS

1.	Confirm access to an FENXT environment with ability to access APPLICATIONS in the FENXT Control Panel
      •	It will be necessary to add an “application” to the FENXT instance, which will connect the custom Power Platform connector to that specific instance
      
2.	Configure access to MS Power Automate with login
      •	A version of Microsoft (Office) 365 that includes MS Power Platform is required
      •	FENXTCustom Connector will be accessible through Power Automate (Flow) and Power Apps
      •	Go to https://us.flow.microsoft.com/ and confirm the ability to login


CREATE NEW APPLICATION AT BLACKBAUD DEVELOPER SITE

1.	Go to https://developer.blackbaud.com/apps/ and ensure Blackbaud profile is signed in

2.	Click to add a new app, fill in information.  

3.	Once saved, notice the application ID and application secret.  Those will be needed when creating the custom connector.  You can get back to these values at any time by going to https://developer.blackbaud.com/apps/ and opening the application you just created.


![image](https://user-images.githubusercontent.com/70080319/121523030-c1abce80-c9c3-11eb-9859-f1629b4a924e.png)


4.	In the Redirect URIs section, click Edit, Add a redirect URI and then paste:  https://global.consent.azure-apim.net/redirect 

5.	Go to the instance of FENXT that will be integrated.  Click Control Panel, Applications

6.	Click Connect app, paste the Application ID referenced in Step 4

7.	That completes the configuration within Blackbaud… now on to the Connector

CONFIGURE FINANCIAL EDGE NXT CONNECTOR

1.	Download FENXT-Power-Connector.swagger.json file from Github

2.	Log into Microsoft Power Automate at https://flow.microsoft.com

3.	On Left Menu, click Data…  Custom Connectors; Click “New Custom Connector”, and select “Import an OpenAPI file”

4.	Assign a connector name, "FENXT Automate Connector" for instance

5.	Click import and select the FENXT-Power-Connector.swagger.json file that was downloaded

6.    Go to Security tab.  Ensure OAuth 2.0 is selected.  Enter Client ID and Client Secret from the Blackbaud Developer app that was created

7.    Update Refresh URL to mirror the token URL:  https://oauth2.sky.blackbaud.com/token

![image](https://user-images.githubusercontent.com/70080319/121524943-d0938080-c9c5-11eb-8bbb-286b43700da7.png)

8.	At the top, click “CREATE CONNECTOR”, then go to DEFINITION PAGE

9.	On the Definition page, first define a Policy to allow for Oauth 2 authentication to a specific FENT environment.  Scroll down and click, “New Policy”

      a.	Name:  Something like “FE Conn”
      b.	Template:  Set HTTP Header
      c.	Operations:  Leave blank
      d.	Header Name:  Bb-Api-Subscription-Key 
      e.	Header Value:  Enter the Primary Access Key or Secondary Access Key defined at https://developer.blackbaud.com/subscriptions/ 
      f.	Action if header exists:  override
      g.	Run Policy on:  Request  
      
![image](https://user-images.githubusercontent.com/70080319/121525301-29fbaf80-c9c6-11eb-8d48-a4fab869a3c2.png)

10.	Click Update Connector

11.   Test the connection using a standard GET for account or project.  If successful, the connected Financial Edge NXT database is accessible from Power Automate and Power Apps

12.   The Financial Edge Connector is accessible from the 'Custom' section within the 'Add an Action' function of Power Automate

![image](https://user-images.githubusercontent.com/70080319/121526061-09802500-c9c7-11eb-8651-746e77f0d0c8.png)





