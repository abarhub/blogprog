+++
title = "Validation xsd en gérant la résolution des xsd"
date = "2021-08-29"
description = "Validation par xsd en gérant la résolution des xsd"
tags = ["java", "xsd"]
+++

Il faut implementer l'interface LSResourceResolver
```Java
public class ResourceResolver  implements LSResourceResolver {

public LSInput resolveResource(String type, String namespaceURI,
        String publicId, String systemId, String baseURI) {

     // note: in this sample, the XSD's are expected to be in the root of the classpath
    InputStream resourceAsStream = this.getClass().getClassLoader()
            .getResourceAsStream(systemId);
    return new Input(publicId, systemId, resourceAsStream);
}

 }
```
Ensuite, l'appel se fait comme cela :
```Java
// note that if your XML already declares the XSD to which it has to conform, then there's no need to declare the schemaName here
void validate(String xml, String schemaName) throws Exception {

    DocumentBuilderFactory builderFactory = DocumentBuilderFactory.newInstance();
    builderFactory.setNamespaceAware(true);

    DocumentBuilder parser = builderFactory
            .newDocumentBuilder();

    // parse the XML into a document object
    Document document = parser.parse(new StringInputStream(xml));

    SchemaFactory factory = SchemaFactory
            .newInstance(XMLConstants.W3C_XML_SCHEMA_NS_URI);

    // associate the schema factory with the resource resolver, which is responsible for resolving the imported XSD's
    factory.setResourceResolver(new ResourceResolver());

            // note that if your XML already declares the XSD to which it has to conform, then there's no need to create a validator from a Schema object
    Source schemaFile = new StreamSource(getClass().getClassLoader()
            .getResourceAsStream(schemaName));
    Schema schema = factory.newSchema(schemaFile);

    Validator validator = schema.newValidator();
    validator.validate(new DOMSource(document));
}
```
Pour la source (`new StreamSource(...)`), il faut utiliser un InputStream. Si on met à la place un File, la résolution est faites sans passer par le ressourceResolver