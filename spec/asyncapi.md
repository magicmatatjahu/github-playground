# AsyncAPI Specification

#### Disclaimer

test

Part of this content has been taken from the great work done by the folks at the [OpenAPI Initiative](https://openapis.org). Mainly because **it's a great work** and we want to keep as much compatibility as possible with the [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification).

#### Version 2.1.0

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

The AsyncAPI Specification is licensed under [The Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html).

## Introduction

The AsyncAPI Specification is a project used to describe and document message-driven APIs in a machine-readable format. It’s protocol-agnostic, so you can use it for APIs that work over any protocol (e.g., AMQP, MQTT, WebSockets, Kafka, STOMP, HTTP, Mercure, etc).

The AsyncAPI Specification defines a set of files required to describe such an API.
These files can then be used to create utilities, such as documentation, integration and/or testing tools.

The file(s) MUST describe the operations an [application](#definitionsApplication) accepts. For instance, consider the following AsyncAPI definition snippet:

```yaml
user/signedup:
  subscribe:
    $ref: "#/components/messages/userSignUp"
```

It means that the [application](#definitionsApplication) allows [consumers](#definitionsConsumer) to subscribe to the `user/signedup` [channel](#definitionsChannel) to receive userSignUp [messages](#definitionsMessage) produced by the application.

**The AsyncAPI specification does not assume any kind of software topology, architecture or pattern.** Therefore, a server MAY be a message broker, a web server or any other kind of computer program capable of sending and/or receiving data. However, AsyncAPI offers a mechanism called "bindings" that aims to help with more specific information about the protocol.

## Table of Contents
<!-- TOC depthFrom:2 depthTo:4 withLinks:1 updateOnSave:0 orderedList:0 -->

- [Definitions](#definitions)
  - [Application](#definitionsApplication)
  - [Producer](#definitionsProducer)
  - [Consumer](#definitionsConsumer)
  - [Message](#definitionsMessage)
  - [Channel](#definitionsChannel)
  - [Protocol](#definitionsProtocol)
- [Specification](#specification)
	- [Format](#format)
	- [File Structure](#file-structure)
	- [Schema](#schema)
      - [AsyncAPI Object](#A2SObject)
      - [AsyncAPI Version String](#A2SVersionString)
      - [Identifier](#A2SIdString)
      - [Info Object](#infoObject)
      - [Contact Object](#contactObject)
      - [License Object](#licenseObject)
      - [Servers Object](#serversObject)
      - [Server Object](#serverObject)  
      - [Server Variable Object](#serverVariableObject)
      - [Default Content Type](#defaultContentTypeString)  
      - [Channels Object](#channelsObject)
      - [Channel Item Object](#channelItemObject)
      - [Operation Object](#operationObject)
      - [Operation Trait Object](#operationTraitObject)
      - [Message Object](#messageObject)
      - [Message Trait Object](#messageTraitObject)
      - [Tags Object](#tagsObject)
      - [Tag Object](#tag-object)
      - [External Documentation Object](#externalDocumentationObject)
      - [Components Object](#componentsObject)
      - [Reference Object](#referenceObject)
      - [Schema Object](#schemaObject)
      - [Security Scheme Object](#securitySchemeObject)
      - [Security Requirement Object](#security-requirement-object)
      - [OAuth Flows Object](#oauth-flows-object)  
      - [OAuth Flow Object](#oauth-flow-object)
      - [Server Bindings Object](#serverBindingsObject)
      - [Parameters Object](#parametersObject)
      - [Parameter Object](#parameterObject)
      - [Channel Bindings Object](#channelBindingsObject)
      - [Operation Bindings Object](#operationBindingsObject)
      - [Message Bindings Object](#messageBindingsObject)
      - [Correlation ID Object](#correlationIdObject)
      - [Specification Extensions](#specificationExtensions)

<!-- /TOC -->

## <a name="definitions"></a>Definitions

#### <a name="definitionsApplication"></a>Application
An application is any kind of computer program or a group of them. It MUST be a [producer](#definitionsProducer), a [consumer](#definitionsConsumer) or both. An application MAY be a microservice, IoT device (sensor), mainframe process, etc. An application MAY be written in any number of different programming languages as long as they support the selected [protocol](#definitionsProtocol). An application MUST also use a protocol supported by the server in order to connect and exchange [messages](#definitionsMessage). 

#### <a name="definitionsProducer"></a>Producer
A producer is a type of application, connected to a server, that is creating [messages](#definitionsMessage) and addressing them to [channels](#definitionsChannel). A producer MAY be publishing to multiple channels depending on the server, protocol, and use-case pattern.
