
<div style="background-color:#5A0F1B;color:white; vertical-align: middle; text-align:center;font-size:190%; padding:10px; margin-top:100px">
 Workshop Pivotal Cloud Foundry & Google Apigee 
</div>

---
# Technical Workshop Pivotal Cloud Foundry & Google Apigee

<img src="img/apigee-pivotal-cloud-foundry.png" width="500" height="339">

## Goal of this material
This material has been created for Pivotal Cloud Foundry (PCF) and Google Apigee workshops.
**It consists in technical labs**, which will guide you in order to make you discover a typical usage of the 2 solutions.
The use case you will work on is called **"JAG"**: Just Another Gateway.
In order to understand this use case, we have created a step-by-step lab.
At this point of the workshop, please be sure instructors have provided the following topics:
    - access to an Apigee Edge demo organization, which is the Apigee Edge (SaaS) tenant you will work on. 
    - access to an PCF demo account, which is the place to create your Euro-Dollar application.

The Euro-Dollar application (aka **eurodol**) is a simple Java application that is able to convert currencies: Euro into Dollar and vice versa. 
Let's get started, and feel free to ask for any questions during the completion of the lab.

# Table of Content

PCF & Google Apigee Workshop

1. Step 1 - Access your PCF - Pivotal Cloud Foundry demo account - !!!!!
    - 1.1 Deploy the **eurodol** application
    - 1.2 Test the **eurodol** application
2. Step 2 - API Creation on the Apigee Edge SaaS platform
    - 2.1 Connect to your Apigee organization
    - 2.2 Upload the OpenAPI **eurodol-v1** specification
    - 2.3 Create an API Proxy, based on your OpenAPI **eurodol-v1** specification
    - 2.4 Modify the configuration of your API Proxy
3. Step 3 - Test your API Proxy using the Trace & Debug tool
    - 3.1 Add Traffic Management (**Quota Enforcement**) and Security (**Verify API Key**) policies to your API Proxy
4. Step 4 - Package your API Proxy into an API Product in Apigee Edge
    - 4.1 Create a developer
    - 4.2 Create an application
    - 4.3 Create an **API Product** 
5. Step 5 - Create your own API Developer Portal
    - 5.1 Instanciate a Developer Portal from your Apigee Edge organization
6. Step 6 - Publish your API Product into your API Developer Portal
    - 6.1 Publish your eurodol API Product
    - 6.2 Generate doc using the OpenAPI **eurodol-v1** specification
7. Step 7 - Test your API Product from the Developer Portal
    - Connect to your Developer Portal
    - Create an account an your Developer Portal
    - Activate your account and sign in
    - Create an Application on your Developer Portal
    - Subscribe to the **eurodol** API Product
    - Test your API Product
    - Verify the Quota Enforcement is enforced
8. Step 8 - Use the API Product and Application on your PCF demo account - !!!!!
9. Step 9 - Analytics and API Monitoring in Apigee Edge
    - 9.1 Connect your Apigee organization
    - Switch to the Analytics Tab
    - Discover the Analytics for your API Proxy and API Product
    - Discover the API Monitoring capabilities of the Apigee API Managemnent platformn
10. Step 10 - Wrap Up


    Appendix A. Apigee Edge Resources

    - 4 minute video 4 developers
    - Apigee docs: 
    - Apigee community: 

    Appendix B. Pivotal Cloud Foundry Resources


# 1. Step 1

This chapter introduces step 1:

## Step 1.1

### Step 1.1.1

```code
ubuntu$ echo "Hello World!!!"
Hello World!!!
```


# 2. Step 2 - API Creation on the Apigee Edge SaaS platform

In this section, you connect to the Apigee Edge platform using your own account. After a quick introduction to the Apigee platform and main tabs, you start creating your first API Proxy and set its configuration.


## Step 2.1 - Connect to your Apigee organization
Before starting this lab, instructors have created an Apigee Edge (SaaS) demo account for each participant.
Accounts have been created with your email addresses. 
As a participant, please connect to your email inbox and activate your demo account, if not completed yet.

At this point, you should be able to access the Apigee Edge login screen, as shown here:

<img src="img/211-login-screen.png">

Once you are connected, you should be able to see the Apigee Edge home page, note that you work in the **emea-poc7** organization, as shown on the following picture:

<img src="img/212-apigee-org.png">

Here is an overview of the Apigee Edge home page:

<img src="img/213-apigee-home.png">

Also note that you are working with an __Organization Admninistrator__ role.

As, you can see, the home page consists in several icons:
- Specs : this is the place where you upload all your OpenAPI specification files. Then you can use these files to create API Proxies
- API Proxies : at this point, just consider an API Proxy as an "API Façade", on which you can add technical controls, in the form of mediation, traffic management, security policies as well as extensions.
- API Products : an API Product is a way to package a set of API Proxies. It can be used to define quotas, custom attributes, OAuth20 scopes and some other specific properties: visibility on the Developer Portal, approval mecahnism for application subscription...
- Portals : once you have created API Products, you can make them available through a Developer Portal

We have just covered here some aspects of an API life cycle...from the Design to the publication of product on a Developer Portal !

## Step 2.2 -  Upload the OpenAPI eurodol-v1 specification

Click on the **Specs** icon, or access the **specs** tab, as shown here:

<img src="img/221-specs-tab.png">

Click the **+Spec** button on the right and top side of the panel, as shown on the image, then select **Import URL...** :

<img src="img/222-plus-spec-button.png">

As **Import Name**, please enter a name of your convenience. Please be aware that this organization is also used by the other participants so you have to find a way to make the name of your file unique! Be creative, for instance you can add your initials to the name of the file: **eurodol-v1_YOUR-INITIALS** (eurodol-v1_jog in my case)

As **Import Url**, please copy and paste the following value: https://raw.githubusercontent.com/JoelGauci/pcf-apigee/master/apigee/specs/eurodol-v1.yaml

This points to the OpenAPI specification we use in this workshop. You can have a look at the specification if you click on the following link:

[eurodol-v1 OpenAPI specification](https://raw.githubusercontent.com/JoelGauci/pcf-apigee/master/apigee/specs/eurodol-v1.yaml)

Before clicking the **Import** button, you should check you get the following info (except the initials...), as shown on the picture: 

<img src="img/223-spec-import.png">

You can now click the **Import** button to import the OpenAPI specification into the orgqnization.

From the Specs list, find your **eurodol-v1** personal specification and click on it, as shown on the following picture:

<img src="img/224-open-spec.png">

This will show the content of your **eurodol-v1** specification, as shown here after:

<img src="img/225-eurodol-spec.png">

Important: you have to make a modification on this file...See the **{YOUR_PERSONAL_CODE}** pattern in the file...you should find it around line 16...

<img src="img/226-perso-pattern.png">

...modify the pattern with your own initials or a pattern of your convenience (do not include any special characters).
Please take note of these initials as you will have to use them later in the workshop.

```code
/{YOUR_PERSONAL_CODE}/api/v1
```

becomes

```code
/jog/api/v1
```

Here is an example of the result in my case, when using the initials **jog**:

<img src="img/227-jog-pattern.png">

Note that the base path starts with a '/'

Once you have made this change on the **eurodol-v1** specification, you can save it, clicking on the **Save** button on the right side of the screen, as shown here:

<img src="img/228-save-spec.png">

You should see a message, which confirms that the document has been saved

## Step 2.3 - Create an API Proxy, based on your OpenAPI **eurodol-v1** specification

Click the **API Proxies** tab from the section list, as shown on the following picture:

<img src="img/231-goto-apiproxies.png">

Then click on the **+Proxy** button on the right side of the screen, as shown here:

<img src="img/232-plus-apiproxy.png">

Select the **Reverse proxy** option and click the **Use OpenAPI** button as shown below:

<img src="img/233-reverse-proxy.png">

From the **My Specs** list, select your own and personal **eurodol-v1** specification and click the **Select** button

Then click the **Next** button, as shown on the following picture:

<img src="img/234-reverse-proxy-next.png">

This will start the creation process of your **eurodol** API Proxy...

On the next panel, please make some modification to make your API Proxy and its base path unique:
1. Add your initials to the name of the API Proxy: **eurodol-jog** in my case
2. Copy and paste the URI of the **Existing API** URL to the **Proxy Base Path** text field
3. Modify the value of the **Existing API** hostname with the value of your PCF app hostname : **https://eurodol-brash-lemur.cfapps.io** in my case 

Except your own initials and your own PCF app hostname, you should see something like this in term of API Proxy settings:

<img src="img/235-apiproxy-settings.png">

If everything is checked on your side, you can click the **Next** button

Verify that the **GET /convert** resource will be exposed by the API Proxy. The check box must be selected and you can click the **Next** button, as shown on the following picture:

<img src="img/236-apiproxy-convert.png">

Then, select the **Pass through (none)** option and click **Next**, as shown here:

<img src="img/237-apiproxy-passthru.png">

Then, unselect the **default** virtual host as we only want to provide secured connection with our API Proxy and click **Next**, as shown here:

<img src="img/238-apiproxy-secure.png">

On the 2 other screens, just select the default options and click **Next**. You should then see a deployment status indicating that the deployment is successful. At this point, click on the name of your API Proxy, as shown on the following image:

<img src="img/239-apiproxy-status.png">

This will allow to access the configuration overview of your API Proxy, as shown here:

<img src="img/23A-apiproxy-overview.png">

## Step 2.4 Modify the configuration of your API Proxy

In this section, you will modify the configuration of your existing **eurodol** API Proxy in order to be able to test it from an API Developer Portal and from a Web browser based application.

CLick the **DEVELOP** tab of you API Proxy menu, as shown here:

<img src="img/241-apiproxy-develop.png">

From this tab, you can access the configuration details of your API Proxy.
First and foremost, we need to add a mediation policy that will handle CORS (Cross Origin Resource Sharing) on our API P{roxy}. Click the **+** button on the **Policies** item on the left side of the panel, as shown on the following picture:

<img src="img/242-apiproxy-addpolicy.png">

Select the **Assign Message Policy**, keep the default value (as display name and name for the policy) and click the **Add** button, as shown here after:

<img src="img/243-apiproxy-addAM.png">

This will create an Assign Message policy (a specific type of mediation policy) in the list of available policies, as shown on the following image:

<img src="img/244-apiproxy-AM.png">

Click the policy and you will access its XML configuration:

<img src="img/245-apiproxy-AM-xmlconfig.png">

All the policies in Apigee are based on an XML configuration. 
Copy the content of the following XML configuration, from the link below:
[Add-CORS.xml](https://raw.githubusercontent.com/JoelGauci/pcf-apigee/master/apigee/config/Add-CORS.xml)

... or from the following code section:

```code
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AssignMessage async="false" continueOnError="false" enabled="true" name="Add-CORS">
    <DisplayName>Add CORS</DisplayName>
    <FaultRules/>
    <Properties/>
    <Set>
        <Headers>
            <Header name="Access-Control-Allow-Origin">*</Header>
            <Header name="Access-Control-Allow-Headers">origin, x-requested-with, accept, content-type, x-apikey</Header>
            <Header name="Access-Control-Max-Age">3628800</Header>
            <Header name="Access-Control-Allow-Methods">GET, PUT, POST, DELETE</Header>
        </Headers>
    </Set>
    <IgnoreUnresolvedVariables>true</IgnoreUnresolvedVariables>
    <AssignTo createNew="false" transport="http" type="response"/>
</AssignMessage>
```

...and paste it in the policy panel, as shown here:

<img src="img/246-apiproxy-AM-copygit.png">

You can check that the name of the Assign Message policy has changed. It is now **Add CORS**, as shown on the list of policies:

<img src="img/247-apiproxy-AM-name.png">


---
<div style="background-color:#5A0F1B;color:white; vertical-align: middle; text-align:center;font-size:190%; padding:10px; margin-top:100px">
</div>
