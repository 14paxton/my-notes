---
title:        Text_Manipulation
permalink: GrailsNotes/Text_Manipulation
category: GrailsNotes
parent: GrailsNotes
layout:       default
has_children: false
share:        true
shortRepo:

  - GrailsNotes
- default

---

<br/>

<details markdown="block">                
<summary>    
Table of contents    
</summary>    
{: .text-delta }    
1. TOC    
{:toc}    
</details>

<br/>

---

<br/>

# Server Side

## GRAILS TYPE Converters

> Convert and check type in controller

> [TypeCheck](http://docs.grails.org/latest/guide/theWebLayer.html#typeConverters)

```groovy
param.short(var)
param.byte(var)
param.long(var)
param.double(var)
param.boolean(var)
```

## JSON

### JSON Parser Example

> This is your JSON object that should be passed in to the method

```groovy

def json = '''{
                  "markings": {
                      "headMarkings": "Brindle",
                      "leftForeMarkings": "",
                      "rightForeMarkings": "sock",
                      "leftHindMarkings": "sock",
                      "rightHindMarkings": "",
                      "otherMarkings": ""
                   }
                }'''

def jsonObj = grails.converters.JSON.parse(json)
```

```groovy
print jsonObj
//optput [markings:[rightForeMarkings:sock, otherMarkings:, leftForeMarkings:, leftHindMarkings:sock, rightHindMarkings:, headMarkings:Brindle]]

def jsonStr = jsonObj.toString()

//This is the string which should be persisted in db
assert jsonStr == '{"markings":{"rightForeMarkings":"sock","otherMarkings":"","leftForeMarkings":"","leftHindMarkings":"sock","rightHindMarkings":"","headMarkings":"Brindle"}}'

//Get back json obj from json str
def getBackJsobObj = grails.converters.JSON.parse(jsonStr)

assert getBackJsobObj.markings.leftHindMarkings == 'sock'
```

# Frontend manipulation

## Using messageSource

[i18n Docs](https://docs.grails.org/4.0.1/guide/i18n.html)

```groovy
 messageSource.getMessage('batch.user.registration.confirmation.message', [jobId as String].toArray(), LocaleContextHolder.locale)
```

## Render grails tags to return in controller

```groovy
render g.select(from: languages, optionKey: "key", optionValue: "value", name: "languageChoice", class: "form-control", value: assessmentLanguage)
```

## save grails tag in variable and render on page

```groovy
"${yourTag.encodeAsRaw()}"
```

> or

```groovy
"${raw(user.description)}"
```

## JSON

### Javascript manipulation

```html

<script>
    const catalogsByType = null;
</script>
<g:applyCodec encodeAs="none">
    catalogsByType = ${resultCatalogs.catalogsByType as grails.converters.JSON};
</g:applyCodec>
<script>
    let data = $
    {raw(data)}

</script>
```