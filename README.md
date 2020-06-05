# Allignemnt with EBSI v1
Information required for tracking alignment of Alastria (AlastriaID and other core components) with EBSI version 1.

## ESSIF (European Self Sovereign Identity Framework) APIs

### DID API
In EBSI V1 all the users (citizens or public organisations) of the platform have generated a unique DID. For public organisations, the DID identifier (together with other attributes, like the associated eIDAS public key ) is also registered in the DID Registry Smart Contract. **For citizens, there is no such type of registration** in the smart contract. However, the DID API resolves the DID document in both cases. 

The API principal function is to retrieve the DID document associated to a specific DID identifier.

The DID API Swagger is [here](https://api.ebsi.xyz/docs/?urls.primaryName=DID%20API).

### Verifiable Credential API
The main functions are:

* Create a W3C Verifiable Credential without proof based on the type and content specified in the credential Subject field. The resulting VC is ready for signing (by the wallet service).

* Validate the VC format, signature, and checks that the issuers are authorised to issue the given credential (by using the Trusted Issuers Registry API).

The Verifiable Credential Swagger API is [here](https://api.ebsi.xyz/docs/?urls.primaryName=Verifiable%20Credential%20API).

### Verifiable Presentation API
The main functions are:

* To create a W3C Presentation (without proof) from the provided credentials. The resulting presentation is ready for signing (by the wallet service).

* To validate the verifiable presentation format and the signature.

The Verifiable Presentation Swagger API is [here](https://api.ebsi.xyz/docs/?urls.primaryName=Verifiable%20Presentation%20API).

### EBSI DID Auth
This service allows for a Digital Identity (DID) to be authenticated in an exchange between parties. This is a particular implementation of the public DID Auth method (https://identity.foundation/working-groups/authentication.html) and it is customized to work with the EBSI network and EBSI DID methods.

For this reason there is not Swagger API here.

### Identity Hub API
This is a core service of the EBSI platform providing the capability of securely storing and accessing the W3C Verifiable Credentials/Attestations in a storage space fully controllable by the user (holder of the VCs/VAs).
Identity hub is an open-source project developed by the Decentralised Identity Foundation (DIF) which aims to provide high availability of personal data storage solution for users.

The API is built to be Restful and its principal functions are that it:

* retrieves the complete list of attributes for a given user, based on its DID (decentralised identifier);

* retrieves the Identity Attributes, from a given user DID, that matches the attributes types specified;

* adds a new Identity Attribute to the repository for the given user DID

* retrieves the Identity Attributes that corresponds to a specific hash.

Note: EBSI V1 implements only the functionality to add new identity attributes, but not to update or delete them.

The Identity HUB Swagger API is [here](https://api.ebsi.xyz/docs/?urls.primaryName=Identity%20Hub%20API)

### Trusted Issuers Registry API
This is a Core Service of the EBSI platform verifying if a legal entity is authorised to issue a W3C Verifiable Credential. The first implementation of this service in EBSI V1 checks for the presence of issuers DID in a Trusted Issuers Smart Contract and verifies if they are allowed to issue specific Verifiable Credentials.

Note: For EBSI V1 only the Get Methods (to read the registry) are implemented. The methods to add new entities in the registry was not developed and it is done manually by the administrator. 

The API is built to be Restful and its principal functions are:

* get issuer by its Decentralised Identifier;

* list of trusted issuers.

The Trusted Issuers Registry Swagger API is [here](https://api.ebsi.xyz/docs/?urls.primaryName=Trusted%20Issuers%20Registry%20API).

### Wallet API
The Wallet API service exposes the interfaces for a wallet common application to operate with the EBSI network.

The API is restful and the functions are:

* Auth Manager:

  * Sessions: Wallet authentication service for users and components/services. 

* Secure Enclave:

  * Signatures: Sign the payload and encode the signature into JWS.
  * Signature: Validations; Validate JSON Web Signature.

* Notifications (used only by the current implementation of the wallet web client):

  * Notifications: Add and retrieve notifications.

  * Notification/accept: Accepted notification from the UI wallet to execute the proper instruction (write to the ledger, store to ID HUB, etc.).

The Wallet Swagger API is [here](https://api.ebsi.xyz/docs/?urls.primaryName=Wallet%20API).
