<a id="top"></a>
[Home](/) | Getting Started

# Getting Started #

If you are new to publishing schema.org, here are some general tips to getting started.

* [Data Types](#data-types)
  * [Literal data types](#data-types_literals)
    * [Text](#data-types_Text)
    * [Number](#data-types_Number)
    * [URL](#data-types_URL)
    * [Boolean](#data-types_Boolean)
    * [Date](#data-types_Date)
    * [DateTime](#data-types_DateTime)
    * [Time](#data-types_Time)
    * [HTML](#data-types_HTML)

<a id="data-types"></a>
## Data Types ##

For each schema.org type, such as Person or Event, there are fields that let you specify more information about that type. Each of these fields has an expected data type that is defined in the documentation as you can see from [Figure 1.](#figure-1).

<a id="figure-1"></a>
<p align="center">
  <strong>Figure 1. schema.org field data types</strong><br/>
  <img src="/assets/schemaorg-datatypes.png">
  <em>The expected data type for each field appears in the middle column. The left column is the name of the field, the middle column is the data type, and the right column is the field's description.</em>
</p>

Every data type is either a *resource* or a *literal*. Resources refer to other schema.org types. For example a Dataset type has a field called author of which the data type can be either a Person or an Organization. Because Person and Organization are other schema.org "types" who have their own fields, they are called resources. In JSON-LD, you specify resources by using curly brackets ```{}```:

<pre>
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  <strong>"author": {
    "@type": "Person",
    "name": "Jane Goodall"
  }</strong>
}
</pre>

In the JSON-LD above, the 'author' is a resource of type 'Person'. Fields that simply have a value are called literal data types. For examples, the 'Person' type above has a 'name' of "Jane Goodall" - a literal text value. 

<a id="data-types_literals"></a>
## Literal Data Types ##

Schema.org defines six literal, or primitive,  data types: [Text](https://schema.org/Text), [Number](https://schema.org/Number), Boolean](https://schema.org/Boolean), [Date](https://schema.org/Date), [DateTime](https://schema.org/DateTime), and [Time](https://schema.org/Time). [Text](https://schema.org/Text) has two special variations: [URL](https://schema.org/URL) and how to specify when text is actually [HTML](#data-type_HTML).  

When using schema.org, literal data types are not not specified using curly brackets ```{}``` as these are resrved for specifying 'objects' or 'resources' such as other schema.org types like ```Person```, ```Organization```, etc. First, let's see how to use a primitive data type by using fields of [CreativeWork](https://schema.org/CreativeWork), the superclass for [Dataset](https://schema.org/Dataset). 

<a id="data-types_Text"></a>
### Text ###
Imagine we want to say the name of our Creative Work is "Passenger Manifest for H.M.S. Titanic". The [name](https://schema.org/name) field of CreativeWork specifies that it expects Text as the data type. We would use it in this way:

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  <strong>"name": "Passenger Manifest for H.M.S. Titanic"</strong>
}
</pre>

<a id="data-types_Number"></a>
### Number ###
Let's say we want to specify the version number of our manifest using the [version](https://schema.org/version) field of CreativeWork which expects a Number. To specify numbers in JSON-LD, we omit the quotations surrounding the value:

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  <strong>"version": 1</strong>
}
</pre>

<a id="data-types_URL"></a>
### URL ###
Now, let's specify the URL of our manifest using the [url](https://schema.org/url) field of CreativeWork, an inheritied field from [Thing](https://schema.org/Thing). This fields expects a valid URL represented as Text:

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  <strong>"url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv"</strong>
}
</pre>

<a id="data-types_Boolean"></a>
### Boolean ###
Using the Boolean value, we can speficy that our manifest is accessible for free using the field [isAccessibleForFree](https://schema.org/isAccessibleForFree) by using the text ```true``` or ```false``` and omitting the quotes:

<pre>
{
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  "url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv",
  <strong>"isAccessibleForFree": true</strong>
}
</pre>

<a id="data-types_Date"></a>
### Date ###

To specify the [datePublished](https://schema.org/datePublished), which allows either a Date or DateTime, as a Date, we can use any [ISO 8601 date format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations) by wrapping the date in double-quotes:

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  "url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv",
  "isAccessibleForFree": true,
  <strong>"datePublished": "2018-07-29"</strong>
}
</pre>

<a id="data-types_DateTime"></a>
### DateTime ###

To specify the [dateModified](https://schema.org/dateModified) as a DateTime, as a Date, we must follow the [ISO 8601  format for combining date and time representations](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations) using the form ```[-]CCYY-MM-DDThh:mm:ss[Z|(+|-)hh:mm] ```:

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  "url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv",
  "isAccessibleForFree": true,
  "datePublished": "2018-07-29",
  <strong>"dateModified": "2018-07-30T14:30Z"</strong>
}
</pre>

<a id="data-types_Time"></a>
### Time ###

[Time](https://schema.org/Time) is a rarely-used data type because it must represent a point in time recurring on multiple days following the [XML Schema definition](https://www.w3.org/TR/xmlschema-2/#time) using the form ```hh:mm:ss[Z|(+|-)hh:mm]``` (see XML schema for details).

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  "url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv",
  "isAccessibleForFree": true,
  "datePublished": "2018-07-29",
  <strong>"dateModified": "2018-07-30T14:30Z"</strong>
}
</pre>

<a id="data-types_HTML"></a>
### HTML ###

The HTML data type is a special variation of the ```Text``` data type. In some cases where `Text` is the expected data type, our actual data type may be HTML (because we are dealing with web pages). In this case, the [schema.org JSON-LD context](https://schema.org/docs/jsonldcontext.json) defines ```HTML``` to mean [rdf:HTML](http://www.w3.org/1999/02/22-rdf-syntax-ns#HTML), the data type for specifying that a string of text should be interpreted as HTML. Let's say that we have a description of our manifest and want to use the [description](https://schema.org/description) field, but we have HTML inside that text. Using the text field as we did above for the ```name``` field, we would specify the ```description``` as: 

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  "url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv",
  "isAccessibleForFree": true,
  "datePublished": "2018-07-29",
  "dateModified": "2018-07-30T14:30Z",
  <strong>"description": "&lt;h3&gt;Acquisition&lt;/h3&gt;&lt;p&gt;The data was acquired from an office outside of &lt;a href\"https://en.wikipedia.org/wiki/New_York_City\"&gt;New York City&lt;/a&gt;."</strong>
}
</pre>

However, to specify that the ```description``` field should be *interpreted* as HTML, you specify ```description``` as a resource, setting the ```@type``` of that resource to "HTML" and placing the HTML string in a JSON-LD property ```@value```:

<pre>
{
  "@context": "https://schema.org",
  "@type": "CreativeWork",
  "name": "Passenger Manifest for H.M.S. Titanic",
  "version": 1,
  "url": "https://raw.githubusercontent.com/Geoyi/Cleaning-Titanic-Data/master/titanic_original.csv",
  "isAccessibleForFree": true,
  "datePublished": "2018-07-29",
  "dateModified": "2018-07-30T14:30Z",
  "description": { 
    <strong>"@type": "HTML", 
    "@value": "&lt;h3&gt;Acquisition&lt;/h3&gt;&lt;p&gt;The data was acquired from an office outside of &lt;a href\"https://en.wikipedia.org/wiki/New_York_City\"&gt;New York City&lt;/a&gt;."</strong> 
  }
}
</pre>

*NOTE: As of 7/28/2018, the [Google Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool/u/0/) understands the value of ```description``` to be `rdf:HTML`, but the tool specifies this type is unknown. However, you can see from the schema.org Github repository, that this method was discussed and implemented in [pull #1634: alias HTML to rdf:HTML](https://github.com/schemaorg/schemaorg/pull/1634)*