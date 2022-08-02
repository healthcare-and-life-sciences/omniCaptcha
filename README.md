<h1>A-HLS OmniCaptcha* *Documentation</h1>

This is a custom lightning web component that leverages Google reCaptcha and can be used in an OmniScript. Typically placed in a OmniScript that is being used on an anonymous Experience Cloud site page.  

<h2>Overview</h2>

omniCaptcha is a custom LWC developed to be used in a OmniScript that is hosted on an Experience Cloud page. It allows you to leverage Google reCAPTCHA for that OmniScript.
[Image: Image.jpg]

<h2>Business Objective</h2>

Google reCaptcha is a tool used to reduce fake form data caused by bots. This component allows those who wish to leverage reCaptcha inside a OmniScript to do so. 

<h3>Business Value and Benefits</h3>

* Cleaner data
* Reduction in development time


<h2>Package Includes:</h2>

*Integration Procedure (1)*

* validate_captcha.json (Importable Datapack)

*Custom Components (2)*

* *omniCaptcha LWC*
    * omniCaptcha.html
    * omniCaptcha.js
    * omniCaptcha.js-meta.xml
* *Custom Head Markup for Experience Cloud site where this will be used*
    * Markup.html


<h2>Configuration Requirements</h2>

<h3>Pre-Installation Steps:</h3>

* You will need to setup a Google account and add your *Fully Qualified Domain Name(s)* (FQDNs) (e.g., www.google.com (http://www.google.com/)) to receive your *Site Key* and *Secret Key* required to add your reCAPTCHA to the OmniScript. *Note*: Do not use any trailing ‘/’ characters when entering your FQDN.
* This Accelerator leverages the *reCAPTCHA v2 checkbox*. 
* More information about reCAPTCHA and creating an API Key can be found at: https://www.google.com/recaptcha/about/.

<h3>Install Configuration Steps:</h3>

**Installation**

* Add the omniCaptcha LWC to your Org using the methods you typically use.  
* Download and import the Integration Procedure

**Configuration**

*Experience Cloud ** *

* You need to navigate to the site settings→Security & Privacy page. 
    * From here set the Security Level to Relaxed
    * Add two Trusted Sites as follows
    * Google – https://www.google.com (https://www.google.com/)
        GStatic – https://www.gstatic.com (https://www.gstatic.com/)

[Image: Image.jpg]
 ** 

* Still in settings navigate to Advanced and click the Edit Head Markup button. 
    * Add the content of the Markup.html file here and click save.  
    * Add your Site Key in this file where it says ENTER_SITE_KEY_HERE
* Navigate to Org Settings→CSP Trusted Sites.
    * Add two sites as follows and ensure that *'Allow site for frame-src'* is checked
    * Google – https://www.google.com (https://www.google.com/)
        GStatic – https://www.gstatic.com (https://www.gstatic.com/)
* Navigate to Org Settings→Remote Site Settings
    * Add the Same two sites as follows
    * Google – https://www.google.com (https://www.google.com/)
        GStatic – https://www.gstatic.com (https://www.gstatic.com/)

*OmniStudio Components*

1. The Data Pack folder in the following GitHub repository contains the Accelerator assets. Please download the assets and save them to your desktop: https://github.com/healthcare-and-life-sciences/omniCaptcha
2. Then, complete the following steps to import the Data Pack into your Salesforce org.
    1. To Import, in your destination Salesforce org, Click on *App Launcher* → Search for '*OmniStudio DataPacks*' and click on it.
    2. Click on '*Installed*' and on the right side click on '*Import from*'.
    3. Select '*From File*' - When the window opens, select the Data Pack file that you downloaded and stored on your machine. Click '*Install*'.

*Integration Procedure*

* Open the validate_captcha Integration Procedure from the Accelerator assets you downloaded.
    * In the second HTTP action node open the REST OPTIONS and add your secret key from Google where it says ENTER_YOUR_SECRET_KEY_HERE

[Image: Image.jpg]
 

    * Save and activate the IP.

*OmniScript*

* Add the Custom LWC input to your OmniScript.  Select omniCaptcha.
    * To enable Debug mode add a  Custom LWC Property of Debug = true
* omniCaptcha will write to the JSON in your OS under the name of the Custom LWC component.  It will create isHuman as either true or false.  
* To hide the next button on the step that includes omniCaptcha you just need to set conditional view of the next step as follows
    * Show Element if True
        * (Step1:CustomLWC1:isHuman = true)

[Image: Image.jpg]
 ** 
*Note: * ** *If the reCAPTCHA fails isHuman will be set to false. * ** *If it succeeds it will be true. ** *
* * ** *Debug data is written to the console of the browser. ** *

For Guest access in Experience Cloud Site

1. Grant access to three apex classes
    1. vlocity_ins.BusinessProcessController
    2. vlocity_ins.BusinessProcessDisplayController
    3. vlocity_ins.PlatformObjectMappings
        
    4. [Image: Image.jpg]
2. Create sharing rule for the OmniScript object and the Guest user of your Experience Site: (The criteria is anything that will always be true)
    1. [Image: Image.jpg]
3. Grant Read access for two objects
    1. vlocity OmniScripts
    2. vlocity OmniScript Compiled Definitions
        1. Grant read access to 'Content' & 'Sequence' fields
            
        2. [Image: Image.jpg]
        3. [Image: Image.jpg]

 

<h2>Assumptions</h2>

1. A customer has licenses for Experience Cloud, Health Cloud, and the HINS Managed Package with OmniStudio.  These solutions have all be installed and are functional.
2. A customer is assuming Salesforce Lightning Experience — not Classic.
3. Data Model elements that are part of the HINS (Vlocity) Managed package and Health Cloud are all available.
4. Experience Cloud assets may include HTML and CSS code.
5. The Accelerator uses the Lightning Design System standards and look. Customers may want to apply their own branding which can be achieved. 
6. Non-authenticated users may have limited access to portal content and features, depending on how a customer has configured its Experience Cloud site.


<h2>Revision History</h2>

* *Revision Short Description (Month Day, Year)*

    * June 1, 2022 - initial version

