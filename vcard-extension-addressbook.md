# AddressBook extension of the W3C vCard ontology

This note extends the [W3C vCard ontology for describing People and Organisations](https://www.w3.org/TR/vcard-rdf/), adding the following terms.
Note that the location and contents of this note may still change before these terms are added to `https://www.w3.org/2006/vcard/ns`.

## https://www.w3.org/2006/vcard/ns#AddressBook
```ttl
:AddressBook a owl:Class ;
    rdfs:label "AddressBook"@en ;
    rdfs:comment "Represents a collection of vCard people and/or vCard groups"@en ;
    rdfs:comment "This class is not part of vCard as defined by the IETF"@en ;
    rdfs:isDefinedBy <https://www.w3.org/2006/vcard/ns> ;
```

Example:
```
@prefix vcard: <http://www.w3.org/2006/vcard/ns#>.
@prefix dc: <http://purl.org/dc/elements/1.1/>.

  <#this> a vcard:AddressBook;
      dc:title "Solid Project Contacts";
      vcard:nameEmailIndex <people.ttl>;
      vcard:groupIndex <groups.ttl>.
<#this> <http://www.w3.org/ns/auth/acl#owner> <https://solidproject.solidcommunity.net/profile/card#me>.
```

## https://www.w3.org/2006/vcard/ns#groupIndex
```ttl
:groupIndex a owl:ObjectProperty ;
    rdfs:label "group index"@en ;
    rdfs:comment "Links an AddressBook to a document containing all its includesGroup properties"@en ;
    rdfs:comment "This property is not part of vCard as defined by the IETF"@en ;
    rdfs:isDefinedBy <https://www.w3.org/2006/vcard/ns> ;
```

Example: see the AddressBook example above.

## https://www.w3.org/2006/vcard/ns#includesGroup
```ttl
:includesGroup a owl:ObjectProperty ;
    rdfs:label "includes group"@en ;
    rdfs:comment "When included in the group index document of an AddressBook, adds the group to the AddressBook"@en ;
    rdfs:comment "This property is not part of vCard as defined by the IETF"@en ;
    rdfs:isDefinedBy <https://www.w3.org/2006/vcard/ns> ;
```

Example:
_addressbook.ttl_:
```ttl
<#this> a vcard:AddressBook;
      vcard:groupIndex <groupIndex.ttl>.
```
_groupIndex.ttl_:
```ttl
<addressbook.ttl#this> a vcard:includesGroup <groups.ttl#group>.
```
_groups.ttl_:
```ttl
<#group> a vcard:Group;
  vcard:fn "Friends";
  vcard:hasMember <person.ttl#this>.
```
_person.ttl_:
```ttl
<#this> a vcard:Individual;
  vcard:fn "John Doe";
  vcard:url [ a vcard:WebID; vcard:value <#this>.
```

## https://www.w3.org/2006/vcard/ns#nameEmailIndex
TBD

## https://www.w3.org/2006/vcard/ns#inAddressBook
TBD

## https://www.w3.org/2006/vcard/ns#WebID
```ttl
:WebID a owl:ObjectProperty ;
    rdfs:label "WebID"@en ;
    rdfs:comment "The WebID of an Individual"@en ;
    rdfs:comment "This property is not part of vCard as defined by the IETF"@en ;
    rdfs:isDefinedBy <https://www.w3.org/2006/vcard/ns> ;
```

Example:
```ttl
<#this> a vcard:Individual;
  vcard:fn "John Doe";
  vcard:url [ a vcard:WebID; vcard:value <#this>.
```
