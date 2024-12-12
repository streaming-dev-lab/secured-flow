<a id="readme-top"></a>

[![Issues][issues-shield]][issues-url]
[![Bug][bug-shield]][bug-url]
[![Feature][feature-shield]][feature-url]
[![Datawise][datawise-shield]][datawise-url]


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="logos/securedflow-nobg.png" alt="Logo" width="300" height="100">
  </a>
  <p align="center">
    Seamless integration into your data pipeline to secure sensitive data fields.
    <br />
    <a href="#getting-started"><strong>Getting Started »</strong></a>
    <br />
    <br />
    <a href="https://github.com/streaming-dev-lab/secured-flow/issues/new">Report Issue</a>
    ·
    <a href="https://github.com/streaming-dev-lab/secured-flow/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    ·
    <a href="https://github.com/streaming-dev-lab/secured-flow/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#overview">Overview</a></li>
    <li>
      <a href="#usage">Usage</a>
      <ul>
        <li><a href="#encryption-algorithms-supported">Encryption Algorithms Supported</a></li>
        <ul>
          <li><a href="#encrypt-aes-(symmetric-key)-usage">AES (Symmetric Key)</a></li>
          <li><a href="#encrypt-rsa-(asymmetric-key)-usage">RSA (Asymmetric Key)</a></li>
        </ul>
        <li><a href="#platforms-supported">Platforms Supported</a></li>
        <ul>
          <li><a href="#apache-kafka">Apache Kafka®</a></li>
          <li><a href="#confluent-platform">Confluent Platform</a></li>
        </ul>
      </ul>
    </li>
    <li>
      <a href="#configuration">Configuration</a>
      <ul>
        <li><a href="#fields">fields</a></li>
        <li><a href="#service">service</a></li>
        <li><a href="#mode">mode</a></li>
        <li><a href="#message.encrypted.format">message.encrypted.format</a></li>
        <li><a href="#message.encrypt.error">message.encrypt.error</a></li>
        <li><a href="#local.encrypt.type">local.encrypt.type</a></li>
        <li><a href="#local.key">local.key</a></li>
        <li><a href="#local.key.location">local.key.location</a></li>
        <li><a href="#local.keystore.password">local.keystore.password</a></li>
        <li><a href="#local.key.password">local.key.password</a></li>
        <li><a href="#local.key.alias">local.key.alias</a></li>
      </ul>
    </li> 
    <li><a href="#limitation">Limitation</a></li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li>
      <a href="#encrypt">Encrypt</a>
      <ul>
        <li><a href="#encrypt-aes-(symmetric-key)">AES (Symmetric Key)</a></li>
        <ul>
          <li><a href="#encrypt-aes-base64-encoded-key">Base64-encoded key</a></li>
          <li><a href="#encrypt-aes-jks">Java KeyStore File (JKS) with Both KeyStore and Key Password</a></li>
        </ul>
        <li><a href="#encrypt-rsa-(asymmetric-key)">RSA (Asymmetric Key)</a></li>
        <ul>
          <li><a href="#encrypt-rsa-pem">Privacy Enhanced Mail File (PEM)</a></li>
          <li><a href="#encrypt-rsa-jks">Java KeyStore File (JKS) with Both KeyStore and Key Password</a></li>
        </ul>
      </ul>
      <a href="#decrypt">Decrypt</a>
      <ul>
        <li><a href="#decrypt-aes-(symmetric-key)">AES (Symmetric Key)</a></li>
        <ul>
          <li><a href="#decrypt-aes-base64-encoded-key">Base64-encoded key</a></li>
          <li><a href="#decrypt-aes-jks">Java KeyStore File (JKS) with Both KeyStore and Key Password</a></li>
        </ul>
        <li><a href="#decrypt-rsa-(asymmetric-key)">RSA (Asymmetric Key)</a></li>
        <ul>
          <li><a href="#decrypt-rsa-pem">Privacy Enhanced Mail File (PEM)</a></li>
          <li><a href="#decrypt-rsa-jks">Java KeyStore File (JKS) with Both KeyStore and Key Password</a></li>
        </ul>
      </ul>
    </li> 
    <li><a href="#encryption-between-the-key-and-value-in-connectrecords">Encryption between the key and value in ConnectRecords</a></li>
      </ul>
    </li> 
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

---

<!-- Overview -->
## Overview

**SecuredFlow** enhances data security with efficient field level encryption, supporting both AES (Symmetric Key) and RSA (Asymmetric Key) encryption methods. Ensure the safety of your critical information throughout its journey in the Apache Kafka® and Confluent Platform.

**SecuredFlow** is the perfect solution for organizations aiming to safeguard their data in the digital era.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<!-- USAGE -->
## Usage
* Configurable Field Selection : Encrypt/Decrypt specific fields based on configuration.

### Encryption Algorithms Supported:

* **<a id="encrypt-aes-(symmetric-key)-usage"></a> AES (Symmetric Key)**: <br/> 
  * Mode : ```GCM```
  * Padding : ```NoPadding```
  * Initialization Vector (IV) : ```96-bit (12-byte)```
  * Authentication tag length : ```128 bit```
  * Provider : ```SunJCE```
  * Accepts keys in :
    * ```Base64-encoded key.```
    * ```Java KeyStore File (JKS) with Both KeyStore and Key Password.```


* **<a id="encrypt-rsa-(asymmetric-key)-usage"></a> RSA (Asymmetric Key)**:
  * Mode : ```ECB```
  * Padding : ```OAEPWithSHA-256AndMGF1Padding```
  * Provider : ```SunJCE```
  * Accepts keys in :
    * ```Privacy Enhanced Mail File (PEM).```
    * ```Java KeyStore File (JKS) with Both KeyStore and Key Password.```

### Platforms Supported:

* **<a id="apache-kafka"></a> Apache Kafka® 3.3+** with Java version 17.
* **<a id="confluent-platform"></a> Confluent Platform : 7.3+** with Java version 17. 
* Additional details about the <a href="https://docs.confluent.io/platform/current/installation/versions-interoperability.html#">compatibility of Apache Kafka® and the Confluent Platform</a>.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<!-- CONFIGURATION -->
## Configuration
| **Name**                                                       | **Default** | **Acceptable**                                | **Require** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------------------------------------------------------|-------------|-----------------------------------------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a id="fields"></a> fields                                     | -           | List of fields                                | ✅           | List of fields to be encrypted or decrypted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| <a id="service"></a> service                                   | -           | ```local-encryption```                        | ✅           | Service to use for encryption.<br/> <br/> **```local-encryption```** : Use a self-generated key for encryption.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <a id="mode"></a> mode                                         | -           | ```encrypt``` <br/> ```decrypt```             | ✅           | Mode to specific SecuredFlow to worked with ```encrypt``` or ```decrypt```.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| <a id="message.encrypted.format"></a> message.encrypted.format | ```byte```  | ```byte``` <br/> ```string```                 | ✅           | Message format after encryption.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| <a id="message.encrypt.error"></a> message.encrypt.error       | ```fail```  | ```fail``` <br/> ```log``` <br/> ```ignore``` | ✅           | Behavior to handle SecuredFlow when meet the error while encryption.<br/><br/> **```fail```** : Force the Connector or Application using SecuredFlow to go down.<br/><br/> **```log```** : Only log an ERROR message, but the Connector or Application using SecuredFlow will continue to run.<br/><br/> **```ignore```** : Ignore the encountered error and continue running the Connector or Application using SecuredFlow as normal.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| <a id="local.encrypt.type"></a> local.encrypt.type             | ```RSA```   | ```AES```<br/> ```RSA```                      | ✅           | Algorithm to specific SecuredFlow to worked. <br/><br/> ```AES``` :  <br/> <li> Mode : ```GCM``` <br/><li>Padding : ```NoPadding```<br/><li> Initialization Vector (IV) : ```96-bit (12-byte)```<br/><li> Authentication tag length : ```128 bit``` <br/><li> Provider : ```SunJCE``` <br/><br/> ```RSA```: <br/> <li> Mode : ```ECB``` <br/><li>Padding : ```OAEPWithSHA-256AndMGF1Padding``` <br/><li> Provider : ```SunJCE``` <br/><br/> **Note** : <br/> <li>If specified as a ```AES```, <a href="#local.key">local.key</a> or <a href="#local.key.location">local.key.location</a> (with ```.JKS```) must also be provided.</li> <br/> <li>If specified as a ```RSA```, <a href="#local.key.location">local.key.location</a> (with ```.JKS``` or ```.PEM```) must also be provided.</li>                                                                                                                                                                                                               |
| <a id="local.key"></a> local.key                               | -           | Base64-encoded key                            | -           | Base64-encoded key for AES encryption.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| <a id="local.key.location"></a> local.key.location             | -           | ```.PEM```<br/>```.JKS```                     | -           | Key file path for encryption<br/><br/> ```.PEM``` :  <br/> <li> Using the ```RSA``` algorithm and the ```SunRsaSign``` provider with ```java.security.KeyFactory``` to read the key from the file. <li> Using ```java.security.spec.X509EncodedKeySpec``` to read the ```PublicKey``` from the file. <li> Using ```java.security.spec.PKCS8EncodedKeySpec``` to read the ```PrivateKey``` from the file. <br/><br/> ```.JKS``` :  <br/> <li> Using the ```JKS``` type and the ```SUN``` provider with ```java.security.KeyStore``` to read the key from the file.<br/><br/>**Note** : <li>For ```AES``` encryption. If <a href="#local.key">local.key</a> is already specified, <a href="#local.key.location">local.key.location</a> will be ignored. </li> <br/> <li>If specified as a ```.JKS``` file, <a href="#local.keystore.password">local.keystore.password</a>, <a href="#local.key.password">local.key.password</a> and <a href="#local.key.alias">local.key.alias</a> must also be provided.</li> |
| <a id="local.keystore.password"></a> local.keystore.password   | -           | Keystore password                             | -           | Keystore password for JKS file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <a id="local.key.password"></a> local.key.password             | -           | Key password                                  | -           | Key password for JKS file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| <a id="local.key.alias"></a> local.key.alias                   | -           | Key alias                                     | -           | Key alias for key in JKS file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |


<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<!-- LIMITATION -->
## Limitation

* Supported only <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/connector/ConnectRecord.html">ConnectRecords</a> (record from <a href="https://docs.confluent.io/platform/current/connect/kafka_connectors.html#">Connector</a>):
  * With **AvroConverter.** (```io.confluent.connect.avro.AvroConverter```)
  * With **ProtobufConverter.** (```io.confluent.connect.protobuf.ProtobufConverter```)
  * With **JsonSchemaConverter.** (```io.confluent.connect.json.JsonSchemaConverter```)<br/><br/>

* Fields to be used for encryption must be:
  * Part of the <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/connector/ConnectRecord.html">ConnectRecords</a> as mentioned above. 
  * **The <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/data/Schema.html">Schema</a> must be either <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/data/Schema.html#STRING_SCHEMA">STRING_SCHEMA</a> or <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/data/Schema.html#OPTIONAL_STRING_SCHEMA">OPTIONAL_STRING_SCHEMA</a>**.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<!-- GETTING STARTED -->
## Getting Started

This is an example of using SecuredFlow to encrypt and decrypt data while it flows through Apache Kafka® and Confluent Platform.

* ### Encrypt

  * **<a id="encrypt-aes-(symmetric-key)"></a> AES (Symmetric Key):**
    * #### <a id="encrypt-aes-base64-encoded-key"></a> Base64-encoded key
        ```Text
        "transforms": "Encrypt"
        "transforms.Encrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Encrypt.fields": "name, nickname"
        "transforms.Encrypt.service": "local-encryption"
        "transforms.Encrypt.mode": "encrypt"
        "transforms.Encrypt.message.encrypted.format": "string"
        "transforms.Encrypt.message.encrypt.error": "fail"
        "transforms.Encrypt.local.encrypt.type": "AES"
        "transforms.Encrypt.local.key": "eKk6hlEH2jo0MrTYQ7IzETPv7eOPLOcrRNsAHgvFb3o="        
        ```
        Input
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```
        Output
        ```json
        {
          "name" : "cF8o3P40NcXXzSMPyO/tGw==",
          "lastname" : "SecuredFlow",
          "nickname" : "9z52wNc/Dahb6MptDizetg==",
          "age" : 25
        }
        ```
      
    * #### <a id="encrypt-aes-jks"></a> Java KeyStore File (JKS) with Both KeyStore and Key Password
        ```Text
        "transforms": "Encrypt"
        "transforms.Encrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Encrypt.fields": "name, nickname"
        "transforms.Encrypt.service": "local-encryption"
        "transforms.Encrypt.mode": "encrypt"
        "transforms.Encrypt.message.encrypted.format": "string"
        "transforms.Encrypt.message.encrypt.error": "fail"
        "transforms.Encrypt.local.encrypt.type": "AES"
        "transforms.Encrypt.local.key.location": "/MFEC/DataWise/SecuredFlow/secretKey.jks"        
        "transforms.Encrypt.local.keystore.password": "P@ssw0rd" 
        "transforms.Encrypt.local.key.password": "P@ssw0rd"               
        "transforms.Encrypt.local.key.alias": "keyAlias"
         ```
      Input
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "E3sWHNFYEZRns+WXZFQa4A==",
          "lastname" : "SecuredFlow",
          "nickname" : "GQanhezkXQ3kSMh0dunEKw==",
          "age" : 25
        }
        ```

  * **<a id="encrypt-rsa-(asymmetric-key)"></a> RSA (Asymmetric Key)**
    * #### <a id="encrypt-rsa-pem"></a> Privacy Enhanced Mail File (PEM)
        ```Text
        "transforms": "Encrypt"
        "transforms.Encrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Encrypt.fields": "name, nickname"
        "transforms.Encrypt.service": "local-encryption"
        "transforms.Encrypt.mode": "encrypt"
        "transforms.Encrypt.message.encrypted.format": "byte"
        "transforms.Encrypt.message.encrypt.error": "fail"
        "transforms.Encrypt.local.encrypt.type": "RSA"
        "transforms.Encrypt.local.key.location": "/MFEC/DataWise/SecuredFlow/key.pem"               
        ```
      Input
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "[B@dbf57b3",
          "lastname" : "SecuredFlow",
          "nickname" : "[B@6973b51b",
          "age" : 25
        }
        ```

    * #### <a id="encrypt-rsa-jks"></a> Java KeyStore File (JKS) with Both KeyStore and Key Password
        ```Text
        "transforms": "Encrypt"
        "transforms.Encrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Encrypt.fields": "name, nickname"
        "transforms.Encrypt.service": "local-encryption"
        "transforms.Encrypt.mode": "encrypt"
        "transforms.Encrypt.message.encrypted.format": "byte"
        "transforms.Encrypt.message.encrypt.error": "fail"
        "transforms.Encrypt.local.encrypt.type": "RSA"
        "transforms.Encrypt.local.key.location": "/MFEC/DataWise/SecuredFlow/key.jks"        
        "transforms.Encrypt.local.keystore.password": "P@ssw0rd" 
        "transforms.Encrypt.local.key.password": "P@ssw0rd"               
        "transforms.Encrypt.local.key.alias": "keyAlias"
         ```
      Input
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "[B@689604d9",
          "lastname" : "SecuredFlow",
          "nickname" : "[B@409bf450",
          "age" : 25
        }
        ```

* ### Decrypt
  * Decryption must use the **same key** as was used during encryption.
  *  The <a href="#message.encrypted.format">message.encrypted.format</a> and <a href="#local.encrypt.type">local.encrypt.type</a> configuration during decryption **must match** the configuration used during encryption. </li> 
  
  * **<a id="decrypt-aes-(symmetric-key)"></a> AES (Symmetric Key):**
    * #### <a id="decrypt-aes-base64-encoded-key"></a> Base64-encoded key
        ```Text
        "transforms": "Decrypt"
        "transforms.Decrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Decrypt.fields": "name, nickname"
        "transforms.Decrypt.service": "local-encryption"
        "transforms.Decrypt.mode": "decrypt"
        "transforms.Decrypt.message.encrypted.format": "string"
        "transforms.Decrypt.message.encrypt.error": "fail"
        "transforms.Decrypt.local.encrypt.type": "AES"
        "transforms.Decrypt.local.key": "eKk6hlEH2jo0MrTYQ7IzETPv7eOPLOcrRNsAHgvFb3o="        
        ```
      Input
        ```json
        {
          "name" : "cF8o3P40NcXXzSMPyO/tGw==",
          "lastname" : "SecuredFlow",
          "nickname" : "9z52wNc/Dahb6MptDizetg==",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        } 
        ```

    * #### <a id="decrypt-aes-jks"></a> Java KeyStore File (JKS) with Both KeyStore and Key Password
        ```Text
        "transforms": "Decrypt"
        "transforms.Decrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Decrypt.fields": "name, nickname"
        "transforms.Decrypt.service": "local-encryption"
        "transforms.Decrypt.mode": "decrypt"
        "transforms.Decrypt.message.encrypted.format": "string"
        "transforms.Decrypt.message.encrypt.error": "fail"
        "transforms.Decrypt.local.encrypt.type": "AES"
        "transforms.Decrypt.local.key.location": "/MFEC/DataWise/SecuredFlow/secretKey.jks"        
        "transforms.Decrypt.local.keystore.password": "P@ssw0rd" 
        "transforms.Decrypt.local.key.password": "P@ssw0rd"               
        "transforms.Decrypt.local.key.alias": "keyAlias"
         ```
      Input
        ```json
        {
          "name" : "E3sWHNFYEZRns+WXZFQa4A==",
          "lastname" : "SecuredFlow",
          "nickname" : "GQanhezkXQ3kSMh0dunEKw==",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```

  * **<a id="decrypt-rsa-(asymmetric-key)"></a> RSA (Asymmetric Key):**
    * #### <a id="decrypt-rsa-pem"></a> Privacy Enhanced Mail File (PEM)
        ```Text
        "transforms": "Decrypt"
        "transforms.Decrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Decrypt.fields": "name, nickname"
        "transforms.Decrypt.service": "local-encryption"
        "transforms.Decrypt.mode": "decrypt"
        "transforms.Decrypt.message.encrypted.format": "byte"
        "transforms.Decrypt.message.encrypt.error": "fail"
        "transforms.Decrypt.local.encrypt.type": "RSA"
        "transforms.Decrypt.local.key.location": "/MFEC/DataWise/SecuredFlow/key.pem"               
        ```
      Input
        ```json
        {
          "name" : "[B@dbf57b3",
          "lastname" : "SecuredFlow",
          "nickname" : "[B@6973b51b",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```

    * #### <a id="decrypt-rsa-jks"></a> Java KeyStore File (JKS) with Both KeyStore and Key Password
        ```Text
        "transforms": "Decrypt"
        "transforms.Decrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
        "transforms.Decrypt.fields": "name, nickname"
        "transforms.Decrypt.service": "local-encryption"
        "transforms.Decrypt.mode": "decrypt"
        "transforms.Decrypt.message.encrypted.format": "byte"
        "transforms.Decrypt.message.encrypt.error": "fail"
        "transforms.Decrypt.local.encrypt.type": "RSA"
        "transforms.Decrypt.local.key.location": "/MFEC/DataWise/SecuredFlow/key.jks"        
        "transforms.Decrypt.local.keystore.password": "P@ssw0rd" 
        "transforms.Decrypt.local.key.password": "P@ssw0rd"               
        "transforms.Decrypt.local.key.alias": "keyAlias"
         ```
      Input
        ```json
        {
          "name" : "[B@689604d9",
          "lastname" : "SecuredFlow",
          "nickname" : "[B@409bf450",
          "age" : 25
        }
        ```
      Output
        ```json
        {
          "name" : "MFEC",
          "lastname" : "SecuredFlow",
          "nickname" : "DataWise",
          "age" : 25
        }
        ```

* ### Encryption between the key and value in ConnectRecords
  * **SecuredFlow** can be applied to **both the key and value of <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/connector/ConnectRecord.html">ConnectRecords</a>** (record from <a href="https://docs.confluent.io/platform/current/connect/kafka_connectors.html#">Connector</a>) : </li>

    * If you want to apply encryption on the **key** of <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/connector/ConnectRecord.html">ConnectRecords</a>  specify configuration ```type``` as follows :
        ```Text
        "transforms": "Encrypt"
        "transforms.Encrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Key"
         ```

    * If you want to apply encryption on the **value** of <a href="https://docs.confluent.io/platform/current/connect/javadocs/javadoc/org/apache/kafka/connect/connector/ConnectRecord.html">ConnectRecords</a> specify configuration ```type``` as follows :
        ```Text
        "transforms": "Encrypt"
        "transforms.Encrypt.type": "org.mfec.kafka.connect.smt.FieldEncrypt$Value"
         ``` 

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<!-- LICENSE -->
## License

There is no license restriction for usage. 

If you require urgent support or need additional encryption features with high priority for your project, please feel free to <a href="#contact">contact us</a> for further consultation. We are more than happy to assist you to the fullest extent.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

<!-- CONTACT -->
## Contact

[![DATAWISE EMAIL][email-shield]][email-url]

[![MFEC_WEBSITE][mfec-shield]][mfec-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[issues-shield]: https://img.shields.io/badge/ISSUE-8A2BE2?style=for-the-badge&label=OPEN&color=yellow
[issues-url]: https://github.com/streaming-dev-lab/secured-flow/issues/new
[bug-shield]: https://img.shields.io/badge/BUG-8A2BE2?style=for-the-badge&label=OPEN&color=orange
[bug-url]: https://github.com/streaming-dev-lab/secured-flow/issues/new?labels=bug&template=bug-report---.md
[feature-shield]: https://img.shields.io/badge/FEATURE-8A2BE2?style=for-the-badge&label=OPEN&color=009900
[feature-url]: https://github.com/streaming-dev-lab/secured-flow/issues/new?labels=enhancement&template=feature-request---.md
[mfec-shield]: https://img.shields.io/badge/WEBSITE-8A2BE2?style=for-the-badge&label=contact&color=blue
[mfec-url]: https://www.mfec.co.th/
[datawise-shield]: https://img.shields.io/badge/DataWise-8A2BE2?style=for-the-badge&logo=googleearth&color=000033
[datawise-url]: https://www.mfec.co.th/en/datawise/
[email-shield]: https://img.shields.io/badge/EMAIL-8A2BE2?style=for-the-badge&label=contact&color=black
[email-url]: mailto:streamingdev-lab@mfec.co.th