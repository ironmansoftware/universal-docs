---
description: Translate strings between languages.
---

# Translations

{% hint style="info" %}
This functionality requires a [license](https://ironmansoftware.com/powershell-universal/).&#x20;
{% endhint %}

Translation support provides the ability to use a special provider to return strings based on the language of the user accessing the API or dashboard.&#x20;

## Defining Strings

Navigate to Platform \ Translations in the Admin Console to define language strings.&#x20;

![](<../.gitbook/assets/image (339).png>)

To define a new language, click Create New Language Translation. The language ID should be the [language ID ](https://en.wikipedia.org/wiki/List\_of\_ISO\_639-1\_codes)that the browser will present when a user accesses the API or dashboard (e.g. `en-US`)

![](<../.gitbook/assets/image (326).png>)

Once you have created the language, you can begin to add strings to it by click Edit. The Key will be used within your scripts and will return the value. The value will change depending on the language.&#x20;

![](<../.gitbook/assets/image (301).png>)

## Using Strings

To use a string, you will take advantage of the new `$tl:` provider. Using this provider in your scripts will automatically translate the key to the string for the user's language.&#x20;

For example, you would use the variable like this.&#x20;

```powershell
$tl:String1
```

The returned value, when the user's locale is en, will be `USA`.&#x20;

Strings are currently available in APIs and dashboards automatically and in scripts when setting the `LanguageID` variable.&#x20;

{% hint style="warning" %}
Note that the `$t:` provider is also available but due to conflicts with the FileSystem provider and mapped T: drives, we suggest using the `$tl:` provider instead. The `$t:` provider will be mapped on machines that do not already have a T: drive mapped.&#x20;
{% endhint %}

## Selecting a Language

PowerShell Universal selects the user's language by examining the `Accept-Language` header in the HTTP request when user's visit the dashboard page or make an API call. If you want to set a language when running a script, you will need to set the `$LanguageID` variable to the language you wish to return.&#x20;

### Fallback Logic&#x20;

If a language is not defined for the specific language ID (e.g. `en-US`), then PowerShell Universal will attempt to locate the next best language. For example, this would then look for `en`.&#x20;

If no language can be found, then the server-wide fallback language will be used. If this hasn't been defined, `en` will be used. You can specify this the fallback language in Settings \ General \ Platform.&#x20;

If no language can be found for the specified key, the key will be returned.&#x20;

## Language Files

Language files are generated in the translations folder within the repository. Each language will have a `.ps1` file named after the language ID. `New-PSUTranslation` is used to define the language and set the strings.&#x20;

It may be desired to edit language files in this way to accommodate copy and pasting keys between language files.&#x20;

![](<../.gitbook/assets/image (422).png>)
