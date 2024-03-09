+++
title = "Heritage de type en xsd"
date = "2024-03-09"
description = "Heritage de type en xsd"
tags = ["xml","xsd"]
summary = "Heritage de type en xsd"
+++
# Heritage de type en XSD

En XSD, il est possible d'utiliser l'heritage de type.

Par exemple :
```xml
<xs:complexType name="AddressType">
    <xs:sequence>
        <xs:element name="Line1" type="xs:string" />
        <xs:element name="Line2" type="xs:string" />
    </xs:sequence>
</xs:complexType>
<xs:complexType name="UKAddressType">
    <xs:complexContent>
        <xs:extension base="AddressType">
            <xs:sequence>
                <xs:element name="County" type="xs:string" />
                <xs:element name="Postcode" type="xs:string" />
            </xs:sequence>
        </xs:extension>
    </xs:complexContent>
</xs:complexType>
<xs:complexType name="USAddressType">
    <xs:complexContent>
        <xs:extension base="AddressType">
            <xs:sequence>
                <xs:element name="State" type="xs:string" />
                <xs:element name="Zipcode" type="xs:string" />
            </xs:sequence>
        </xs:extension>
    </xs:complexContent>
</xs:complexType>
```
Le type UKAddressType contient les champs Line1, Line2, Country et Postcode, alors que le type USAddressType contient les champs Line1, Line2, Stat et Zipcode.

Le type AddressType peut  tre abstract avec l'attribut `abstract="true"`

## Utilisation dans du XSD

Pour utiliser dans du xsd l'un ou l'autre, il faut indiquer le type :
```xml
<xs:element name="UKAddress" type="UKAddressType" />
<xs:element name="USAddress" type="USAddressType" />
```

# Utilisation dans du XML

Pour l'utiliser dans du xml, il faut ajouter l'attribut `xsi:type`.

Par exemple pour le type suivant 
```xml
<xs:element name="Person">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="Name" type="xs:string" />
            <xs:element name="HomeAddress" type="AddressType" />
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

Il peut  tre utilis  comme  a :
```xml
<?xml version="1.0" ?>
<Person>
    <Name>Fred</Name>
    <HomeAddress>
        <Line1>22 whatever place, someplace</Line1>
        <Line2>sometown, ss1 6gy </Line2>
    </HomeAddress>
</Person>
```
ou comme  a :
```xml
<?xml version="1.0" ?>
<Person xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
    <Name>Fred</Name> 
    <HomeAddress xsi:type="USAddressType"> 
        <Line1>234 Lancaseter Av</Line1> 
        <Line2>SmallsVille</Line2> 
        <State>Florida</State> 
        <Zipcode>34543</Zipcode> 
    </HomeAddress> 
</Person>
```

Information trouv  [ici](https://www.liquid-technologies.com/xml-schema-tutorial/xsd-extending-types)
                    