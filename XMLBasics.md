# **XML Basics**
There are different tags that can be used in an xml file. It may contain valid as well as invalid tags.

**But who is going to valid these tags?** - XML Schema Definition. It also takes care of the schema location. 
An XML Schema describes the structure of an XML document. The XML Schema language is also referred to as XML Schema Definition (XSD).

The purpose of an XML Schema is to define the legal building blocks of an XML document:
  - the elements and attributes that can appear in a document
  - the number of (and order of) child elements
  - data types for elements and attributes
  - default and fixed values for elements and attributes

**Why Learn XML Schema?**

In the XML world, hundreds of standardized XML formats are in daily use.Many of these XML standards are defined by XML Schemas.
XML Schema is an XML-based (and more powerful) alternative to DTD.

**XML Schemas Support Data Types**

One of the greatest strength of XML Schemas is the support for data types.
  - It is easier to describe allowable document content
  - It is easier to validate the correctness of data
  - It is easier to define data facets (restrictions on data)
  - It is easier to define data patterns (data formats)
  - It is easier to convert data between different data types

**XML Schemas use XML Syntax**

Another great strength about XML Schemas is that they are written in XML.
  - You don't have to learn a new language
  - You can use your XML editor to edit your Schema files
  - You can use your XML parser to parse your Schema files
  - You can manipulate your Schema with the XML DOM
  - You can transform your Schema with XSLT
  - XML Schemas are extensible, because they are written in XML.

With an extensible Schema definition you can:
  - Reuse your Schema in other Schemas
  - Create your own data types derived from the standard types
  - Reference multiple schemas in the same document
  - XML Schemas Secure Data Communication
  -When sending data from a sender to a receiver, it is essential that both parts have the same "expectations" about the content.

With XML Schemas, the sender can describe the data in a way that the receiver will understand.A date like: "03-11-2004" will, in some 
countries, be interpreted as 3.November and in other countries as 11.March.
However, an XML element with a data type like this:
<date type="date">2004-03-11</date>
ensures a mutual understanding of the content, because the XML data type "date" requires the format "YYYY-MM-DD".

Well-Formed is Not Enough. A well-formed XML document is a document that conforms to the XML syntax rules, like:
  - it must begin with the XML declaration
  - it must have one unique root element
  - start-tags must have matching end-tags
  - elements are case sensitive
  - all elements must be closed
  - all elements must be properly nested
  - all attribute values must be quoted
  - entities must be used for special characters
    
Even if documents are well-formed they can still contain errors, and those errors can have serious consequences.
Think of the following situation: you order 5 gross of laser printers, instead of 5 laser printers. With XML Schemas, most of these
errors can be caught by your validating software.

# **Good to know info** 

**What is a DTD?** - A DTD is a Document Type Definition. A DTD defines the structure and the legal elements and attributes of an XML
document.

**Why Use a DTD?** - With a DTD, independent groups of people can agree on a standard DTD for interchanging data.
An application can use a DTD to verify that XML data is valid.

**An Internal DTD Declaration** - If the DTD is declared inside the XML file, it must be wrapped inside the <!DOCTYPE> definition:

    XML document with an internal DTD
    <?xml version="1.0"?>
    <!DOCTYPE note [
    <!ELEMENT note (to,from,heading,body)>
    <!ELEMENT to (#PCDATA)>
    <!ELEMENT from (#PCDATA)>
    <!ELEMENT heading (#PCDATA)>
    <!ELEMENT body (#PCDATA)>
    ]>
    <note>
    <to>Tove</to>
    <from>Jani</from>
    <heading>Reminder</heading>
    <body>Don't forget me this weekend</body>
    </note>
    
In the XML file, select "view source" to view the DTD.

The DTD above is interpreted like this:
 - !DOCTYPE note defines that the root element of this document is note
 - !ELEMENT note defines that the note element must contain four elements: "to,from,heading,body"
 - !ELEMENT to defines the to element to be of type "#PCDATA"
 - !ELEMENT from defines the from element to be of type "#PCDATA"
 - !ELEMENT heading defines the heading element to be of type "#PCDATA"
 - !ELEMENT body defines the body element to be of type "#PCDATA"

**An External DTD Declaration** - If the DTD is declared in an external file, the <!DOCTYPE> definition must contain a reference to the 
DTD file:
