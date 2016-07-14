---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring custom domain for  {{site.data.keyword.mobilefoundation_short}} server
{: #configcustomdomain}

*Last updated: 20 June 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} provisions a {{site.data.keyword.mfserver_short_notm}} on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to a URL having the  domain names based on the {{site.data.keyword.Bluemix_notm}} **Region**. You can also configure your own custom domain.
{:shortdesc}

A container group is created with a URL or route having the default domain names based on the {{site.data.keyword.Bluemix_notm}} `Region`.

*Table 1. Application domain names based on `Region` in  {{site.data.keyword.Bluemix_notm}}*

  |Domain |  Region  |    
  |:----- | :----- |    
  |`mybluemix.net` | US South |    
  |`eu-gb.mybluemix.net` | United Kingdom  |    

To be able to use your own domain you will need to configure custom domain by performing the following steps:

1.	Create a {{site.data.keyword.mfserver_short_notm}} instance  by creating the {{site.data.keyword.mobilefoundation_short}} service instance by choosing one of the supported plans.

+ Add the custom domain that you would want to use, to your {{site.data.keyword.Bluemix_notm}} `Organization`. Go to **Manage Organizations > DOMAINS > ADD DOMAIN** to add your own domain.

+ Set up a route for the container group to use your custom domain.

+ Go to the DNS provider for your domain, and add a CNAME entry, which will route the traffic from your domain to the default {{site.data.keyword.Bluemix_notm}} route, where the container group is running.

+ If you would like to configure `https` for your custom domain then upload the SSL certificate for your domain in {{site.data.keyword.Bluemix_notm}}. To do this go to **Manage Organizations > DOMAINS**, select the custom domain you want to configure SSL certificate for, click the **Upload Certificate** to upload SSL certificate for your domain. Refer to [SSL Certificates and Bluemix Custom Domains](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/), for more information.
