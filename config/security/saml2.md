---
description: SAML2 authentication for PowerShell Universal.
---

# SAML2

{% hint style="info" %}
SAML2 requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

PowerShell Universal can be configured to integrate with a SAML2 identity provider. This documentation provides the details for configuring PSU with such a system.

## Identity Provider Settings

You will need to configure your identity provider for the PowerShell Universal application. You will need to setup an acceptable entity ID and map attributes. PowerShell Universal requires that the name attribute is mapped. The attribute name needs to be the following.&#x20;

```
http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
```

You should map this to the user identity you wish to be used within PowerShell Universal.&#x20;

Additional attributes can be mapped and will be available during [role evaluation](./#authorization). You will find an example of configuring Shibboleth below.&#x20;

## Entity ID Settings

{% hint style="info" %}
[HTTPS ](../hosting/#configuring-https)is required for SAML2 authentication.&#x20;
{% endhint %}

There are several basic settings you can configure in the PowerShell Universal admin console. To add SAML2 support, click Security \ Authentication. In the top right corner, you can select SAML2 from the drop down.&#x20;

![](<../../.gitbook/assets/image (301).png>)

Once the SAML2 integration has been added, you can configure the basic settings for communicating with your identity provider. You will need at least the Entity ID and Identity Provider Entity ID configured.&#x20;

Typically, these entity IDs are URLs configured within your identity provider.&#x20;

![Entity ID Settings](<../../.gitbook/assets/image (87).png>)

The service certificate is used for signing requests. It is not required. This can either be a path local to the PSU service or the distinguished name of a certificate installed in the Personal Computer Certificate store.&#x20;

## Additional Settings

In addition to the settings available within the admin console, you can also set the following within the `authentication.ps1` config file.&#x20;

### ServiceCertificatePassword

If you are using a file path for your certificate and it requires a password, you can specify it via the `-ServiceCertificatePassword` of `Set-PSUAuthenticationMethod`. The value of this parameter is a `SecureString`. You can take advantage of the SecretManagement module to load secrets.&#x20;

```powershell
Set-PSUAuthenticationMethod `
-Type "Saml2" `
-EntityId "http://psu.ironman.local/sp" `
-IdentityProviderEntityId 'https://ironman.local/idp' `
-MetadataAddress 'https://idp.ironman.local/idp/shibboleth' `
-CallbackPath "https://localhost:5000/" `
-ServiceCertificate cert.pfx `
-ServiceCertificatePassword (Get-Secret -Name 'certPassword')
```

### Configure

The `-Configure` parameter is a script block that can be used to set additional settings not exposed by the `Set-PSUAuthenticationMethod`. The script block will be called when the provider is configured and will receive a single parameter that contains an object with the options for the SAML2 authentication.&#x20;

The object is of the type [Saml2Options](https://github.com/Sustainsys/Saml2/blob/develop/Sustainsys.Saml2.AspNetCore2/Saml2Options.cs). The sub object of SPOptions can be found [here](https://github.com/Sustainsys/Saml2/blob/20990905ecdcf15f6f76fef80506d53831f7857b/Sustainsys.Saml2/Configuration/SPOptions.cs).

```powershell
Set-PSUAuthenticationMethod `
-Type "Saml2" `
-EntityId "http://psu.ironman.local/sp" `
-IdentityProviderEntityId 'https://ironman.local/idp' `
-MetadataAddress 'https://idp.ironman.local/idp/shibboleth' `
-Configure {
  $options = $args[0]
  $options.SPOptions.DiscoveryServiceUrl = 'https://idp.ironman.local/discovery'
}
```

## Example: Azure AD

You will need the following information from Azure AD.&#x20;

Application (client) ID - Found on the Overview page.&#x20;

Federation metadata document - Click Endpoints on the Overview page.&#x20;

SAML-P sign-on endpoint - Click Endpoints on the Overview page.&#x20;

### Step by Step

Click Security \ Authentication.&#x20;

Add SAML2 authentication provider.&#x20;

Click the Edit Properties button.&#x20;

For Entity ID, you will need to put the Azure AD application ID prefixed with `spn:`&#x20;

For example: `spn:2cf33625-e312-4659-a7bd-66ade51a0ea2`

For Identity Provider Entity ID, you will need to retrieve the entity ID from the Federation metadata document. Open the document in a web browser.&#x20;

<figure><img src="../../.gitbook/assets/image (493).png" alt=""><figcaption><p>Entity ID Property</p></figcaption></figure>

For Metadata Address, insert the Federation metadata document URL.

For the Return URL, insert the URL of your PowerShell Universal server with the `/Saml/Acs` path.

```
https://localhost/Saml2/Acs
```

For Single Sign-On Service URL, insert the SAML-P sign-on endpoint from Azure.&#x20;

<figure><img src="../../.gitbook/assets/image (202).png" alt=""><figcaption><p>SAML2 Properties</p></figcaption></figure>



Once complete, save the settings and enable the SAML provider. Click sign out and navigate to your admin console URL.&#x20;

```
https://localhost/admin
```

You will be forwarded to Azure for login and redirected back to PowerShell Universal after authentication.&#x20;

Any errors that occur will be listed in the PowerShell Universal log. If you fail to login, you can navigate to `/login` to login with a local account.

### Ad

## Example: Okta

This example shows how to configure Okta SAML2 authentication for use with PowerShell Universal.&#x20;

Within Okta, you will need to configure your application similar to the following. HTTPS is required by SAML2, and you will need to include the URL for your PSU instance in the Single Sign On URL, followed by `/Saml2/Acs`. The path is case sensitive.&#x20;

The Audience Restriction should be the URL of your PowerShell Universal server.&#x20;

![](<../../.gitbook/assets/image (132).png>)

In order for your users to access PowerShell Universal, you will need to ensure they have been assigned to the Okta application.&#x20;

![](<../../.gitbook/assets/image (131).png>)

Within the Sign On tab of your application, click the View SAML setup instructions button.&#x20;

![](<../../.gitbook/assets/image (382).png>)

You will need to capture the two URLs and download the certificate for configuring PowerShell Universal. See the next step on how to use these URLs within the `authentication.ps1` file.&#x20;

### authentication.ps1

The authentication.ps1 file is used for configuring PowerShell Universal.&#x20;

```powershell
Set-PSUAuthenticationMethod -Type "Saml2" `
-EntityId "https://localhost:5001" `
-IdentityProviderEntityId "http://www.okta.com/exk5dvbyzgASPiOFp5d7" `
-CallbackPath "https://localhost:5001" `
-SigningKey "C:\Users\adamr\Downloads\okta.cert" `
-SingleSignOnServiceUrl "https://dev-36706648.okta.com/app/dev-36706648_psusaml_1/exk5dvbyzgASPiOFp5d7/sso/saml"
```

| Parameter                | Description                                                                                | Type   |
| ------------------------ | ------------------------------------------------------------------------------------------ | ------ |
| EntityId                 | This value should match what you put in Audience Restriction within Okta.                  | string |
| IdentityProviderEntityId | This is the value that was presented in the View SAML setup instructions page.             | string |
| CallbackPath             | This is the path that the user will be redirected to if no redirect path was provided      | string |
| SigningKey               | This is the certificate file that was downloaded on the View SAML setup instructions page. | string |
| SingleSignOnServiceUrl   | This is the sign on URL that was provided on the View SAML setup instructions page.        | string |

## Example: Shibboleth

This example shows how to configure Shibboleth for use with PowerShell Universal. It provides the very basic configuration and does not necessarily follow best practices.&#x20;

This assumes that you have installed Shibboleth Identity Provider v4 with Active Directory integration.&#x20;

### ldap.properties

LDAP properties have been configured to authentication against the local domain using a Domain Administrator account. The LDAP URL has been configured and TLS has been disabled.&#x20;

Below you will find the full example of the `ldap.properties` file.&#x20;

```
# LDAP authentication (and possibly attribute resolver) configuration
# Note, this doesn't apply to the use of JAAS authentication via LDAP

## Authenticator strategy, either anonSearchAuthenticator, bindSearchAuthenticator, directAuthenticator, adAuthenticator
idp.authn.LDAP.authenticator=adAuthenticator

## Connection properties ##
idp.authn.LDAP.ldapURL=ldap://ironman.local:389
idp.authn.LDAP.useStartTLS                     = false
# Time in milliseconds that connects will block
#idp.authn.LDAP.connectTimeout                  = PT3S
# Time in milliseconds to wait for responses
#idp.authn.LDAP.responseTimeout                 = PT3S
# Connection strategy to use when multiple URLs are supplied, either ACTIVE_PASSIVE, ROUND_ROBIN, RANDOM
#idp.authn.LDAP.connectionStrategy               = ACTIVE_PASSIVE

## SSL configuration, either jvmTrust, certificateTrust, or keyStoreTrust
idp.authn.LDAP.sslConfig                       = jvmTrust
## If using certificateTrust above, set to the trusted certificate's path
idp.authn.LDAP.trustCertificates=%{idp.home}/credentials/ldap-server.crt
## If using keyStoreTrust above, set to the truststore path
idp.authn.LDAP.trustStore=%{idp.home}/credentials/ldap-server.truststore

## Return attributes during authentication
idp.authn.LDAP.returnAttributes=passwordExpirationTime,loginGraceRemaining,sn,mail

## DN resolution properties ##

# Search DN resolution, used by anonSearchAuthenticator, bindSearchAuthenticator
# for AD: CN=Users,DC=example,DC=org
idp.authn.LDAP.baseDN=CN=Users,DC=ironman, DC=local
idp.authn.LDAP.subtreeSearch                   = true
idp.authn.LDAP.userFilter=(sAMAccountName={user})
# bind search configuration
# for AD: idp.authn.LDAP.bindDN=adminuser@domain.com
idp.authn.LDAP.bindDN=administrator@ironman.local

# Format DN resolution, used by directAuthenticator, adAuthenticator
# for AD use idp.authn.LDAP.dnFormat=%s@domain.com
idp.authn.LDAP.dnFormat=%s@ironman.local

# pool passivator, either none, bind or anonymousBind
#idp.authn.LDAP.bindPoolPassivator                  = none

# LDAP attribute configuration, see attribute-resolver.xml
# Note, this likely won't apply to the use of legacy V2 resolver configurations
idp.attribute.resolver.LDAP.ldapURL=%{idp.authn.LDAP.ldapURL}
idp.attribute.resolver.LDAP.connectTimeout=%{idp.authn.LDAP.connectTimeout:PT3S}
idp.attribute.resolver.LDAP.responseTimeout=%{idp.authn.LDAP.responseTimeout:PT3S}
idp.attribute.resolver.LDAP.connectionStrategy=%{idp.authn.LDAP.connectionStrategy:ACTIVE_PASSIVE}
idp.attribute.resolver.LDAP.baseDN=%{idp.authn.LDAP.baseDN:undefined}
idp.attribute.resolver.LDAP.bindDN=%{idp.authn.LDAP.bindDN:undefined}
idp.attribute.resolver.LDAP.useStartTLS=%{idp.authn.LDAP.useStartTLS:true}
idp.attribute.resolver.LDAP.trustCertificates=%{idp.authn.LDAP.trustCertificates:undefined}
idp.attribute.resolver.LDAP.searchFilter=(sAMAccountName=$resolutionContext.principal)

# LDAP pool configuration, used for both authn and DN resolution
#idp.pool.LDAP.minSize                          = 3
#idp.pool.LDAP.maxSize                          = 10
#idp.pool.LDAP.validateOnCheckout               = false
#idp.pool.LDAP.validatePeriodically             = true
#idp.pool.LDAP.validatePeriod                   = PT5M
#idp.pool.LDAP.validateDN                       =
#idp.pool.LDAP.validateFilter                   = (objectClass=*)
#idp.pool.LDAP.prunePeriod                      = PT5M
#idp.pool.LDAP.idleTime                         = PT10M
#idp.pool.LDAP.blockWaitTime                    = PT3S

```

### relying-party.xml

The `relying-party.xml` file has been updated to enable open IdP. This means that any entity ID can communicate with the identity provider. You can also configure this to enforce specific entity IDs. The default configure has also been adjusted to use the `SAML2.AttributeQuery` bean.&#x20;

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:util="http://www.springframework.org/schema/util"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd"
                           
       default-init-method="initialize"
       default-destroy-method="destroy">

    <!--
    Unverified RP configuration, defaults to no support for any profiles. Add <ref> elements to the list
    to enable specific default profile settings (as below), or create new beans inline to override defaults.
    
    "Unverified" typically means the IdP has no metadata, or equivalent way of assuring the identity and
    legitimacy of a requesting system. To run an "open" IdP, you can enable profiles here.
    -->
    <bean id="shibboleth.UnverifiedRelyingParty" parent="RelyingParty">
        <property name="profileConfigurations">
            <list>
			<bean parent="SAML2.SSO" p:encryptAssertions="false" />
            </list>
        </property>
    </bean>

    <!-- Default configuration, with default settings applied for all profiles. -->
    <bean id="shibboleth.DefaultRelyingParty" parent="RelyingParty">
        <property name="profileConfigurations">
            <list>
                <!-- SAML 1.1 and SAML 2.0 AttributeQuery are disabled by default. -->
                <!--
                <bean parent="Shibboleth.SSO" />
                <ref bean="SAML1.AttributeQuery" />
                <ref bean="SAML1.ArtifactResolution" />
                -->
                <bean parent="SAML2.SSO" />
                <ref bean="SAML2.ECP" />
                <ref bean="SAML2.Logout" />
                <ref bean="SAML2.AttributeQuery" />
                <ref bean="SAML2.ArtifactResolution" />
                <ref bean="Liberty.SSOS" />
            </list>
        </property>
    </bean>
</beans>

```

### attribute-resolver.xml

The `attribute-resolver.xml` file has been updated to use the LDAPDirectory Data Connector. It loads the email address, given name, SN, and display name from Active Directory. It then maps the Principal Name, which will be the username of the user logging in, to the required claim type using an attribute encoder.&#x20;

```
<?xml version="1.0" encoding="UTF-8"?>
<!--
    This file is an EXAMPLE configuration file containing some example attributes
    based on some commonly used approaches when LDAP is the principal data source.
     
    Not all attribute definitions or data connectors are demonstrated, but some
    LDAP attributes common to Shibboleth deployments (and some not so common) are
    included.

    This example is in no way usable as a substitute for reading the documentation.    
-->
<AttributeResolver
        xmlns="urn:mace:shibboleth:2.0:resolver"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="urn:mace:shibboleth:2.0:resolver http://shibboleth.net/schema/idp/shibboleth-attribute-resolver.xsd">

    <!-- ========================================== -->
    <!--      Attribute Definitions                 -->
    <!-- ========================================== -->

    <!-- Simple attributes are exported directly from the LDAP connector. -->

    <AttributeDefinition id="uid" xsi:type="PrincipalName" />
    <AttributeDefinition id="username" xsi:type="PrincipalName">
         <AttributeEncoder xsi:type="SAML2String" name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name" friendlyName="displayName" encodeType="false" />
    </AttributeDefinition>

    <!-- ========================================== -->
    <!--      Data Connectors                       -->
    <!-- ========================================== -->

    <!-- Example LDAP Connector -->

    <DataConnector id="myLDAP" xsi:type="LDAPDirectory"
        ldapURL="%{idp.attribute.resolver.LDAP.ldapURL}"
        baseDN="%{idp.attribute.resolver.LDAP.baseDN}" 
        principal="%{idp.attribute.resolver.LDAP.bindDN}"
        principalCredential="%{idp.attribute.resolver.LDAP.bindDNCredential}"
        useStartTLS="%{idp.attribute.resolver.LDAP.useStartTLS:true}"
        connectTimeout="%{idp.attribute.resolver.LDAP.connectTimeout}"
        responseTimeout="%{idp.attribute.resolver.LDAP.responseTimeout}"
        connectionStrategy="%{idp.attribute.resolver.LDAP.connectionStrategy}"
        noResultIsError="true"
        multipleResultsIsError="true"
        excludeResolutionPhases="c14n/attribute"
        exportAttributes="mail displayName sn givenName">
        <FilterTemplate>
            <![CDATA[
                %{idp.attribute.resolver.LDAP.searchFilter}
            ]]>
        </FilterTemplate>
        <ConnectionPool
            minPoolSize="%{idp.pool.LDAP.minSize:3}"
            maxPoolSize="%{idp.pool.LDAP.maxSize:10}"
            blockWaitTime="%{idp.pool.LDAP.blockWaitTime:PT3S}"
            validatePeriodically="%{idp.pool.LDAP.validatePeriodically:true}"
            validateTimerPeriod="%{idp.pool.LDAP.validatePeriod:PT5M}"
            validateDN="%{idp.pool.LDAP.validateDN:}"
            validateFilter="%{idp.pool.LDAP.validateFilter:(objectClass=*)}"
            expirationTime="%{idp.pool.LDAP.idleTime:PT10M}"/>
    </DataConnector>

</AttributeResolver>

```

### attribute-filter.xml

The `attribute-filter.xml` file has been updated to release several of the attributes mapped by the LDAPDirectory data connector as well as the user name that will be used as the identity within PowerShell Universal.&#x20;

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- 
    This file is an EXAMPLE policy file.  While the policy presented in this 
    example file is illustrative of some simple cases, it relies on the names of
    non-existent example services and the example attributes demonstrated in the
    default attribute-resolver.xml file.

    This example does contain some usable "general purpose" policies that may be
    useful in conjunction with specific deployment choices, but those policies may
    not be applicable to your specific needs or constraints.    
-->
<AttributeFilterPolicyGroup id="ShibbolethFilterPolicy"
        xmlns="urn:mace:shibboleth:2.0:afp"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="urn:mace:shibboleth:2.0:afp http://shibboleth.net/schema/idp/shibboleth-afp.xsd">

<AttributeFilterPolicy id="example1">
        <PolicyRequirementRule xsi:type="ANY" />
        <AttributeRule attributeID="username">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>
        <AttributeRule attributeID="displayName">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>
        <AttributeRule attributeID="uid">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>
        <AttributeRule attributeID="mail">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>
        <AttributeRule attributeID="sn">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>
    </AttributeFilterPolicy>
 


</AttributeFilterPolicyGroup>

```
