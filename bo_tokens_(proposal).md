# General Questions / Assumptions

Those questions should be solved before introducing the token bo.

 * Is only a RFID whitelist exchange needed/wanted?
 * Do we need method to authorize at the EMP-Backend with an UUID/token instance?
 * Other (future) tokens should be possible?
 * Where is remote-authentication via apps on the roadmap? Does it have influence on the tokens? Should it be interoperable with rfid-whitelist authentication?
 * Where is support for 15118 on the roadmap? Does it have influence on the tokens?
 * Do we want to provide a *session-push*, when a provider's token is presented at an operator's evse? Compare to [OCHP direct](https://github.com/e-clearing-net/OCHP/blob/master/OCHP-direct.md#inform-a-provider-about-a-charging-process-advanced)
 * ...?

---

*This is a template for object descriptions.*

# Business Object Name

*General description of the business object*



## 1. Inheritances

*List all inheritors.*


## 2. Flow and Lifecycle

*Describe the status of the objects, how it is created and destroyed,
when and through which action it gets inherited. Name the owner. Explain
the purpose.*


## 3. Interfaces and endpoints

*Explain which interfaces are available and which party should implement
which one.*


### 3.1 Interface #1

*Describe the interface in detail.*

Endpoint structure /xxx/yyy/

| Method   | Description                                          |
| -------- | ---------------------------------------------------- |
| GET      |                                                      |
| POST     |                                                      |
| PUT      |                                                      |
| PATCH    |                                                      |
| DELETE   |                                                      |




## Object description

*Describe the structure of this object.*

### RoamingContract *class*

Contains information about a roaming authorisation (card/token)

 Field Name     |  Field Type    |  Card.  |  Description
:---------------|:---------------|:--------|:------------
 contract_id    |  ContractId    |  1      |  According to ISO
 group_mode     |  GroupMode     |  +      |  In which mode this group is operated. **NEEDED?**
 features       |  Features      |  ?      |  Which features does the contract is autherized for  **NEEDED?**
 tokens         |  Token*[]      |  +      |  List of various tokens



### Example:


```json
[
    {
        "contract_id": "NL123C00000001",
        "group_mode": "ALL_EQUAL",
        "features": [
            AC_CHARGING,
            DC_CHARGING
        ],
        "tokens": [
            {
                "uuid": "cf3a0fe2715d0",
                "printed_number": "Card 00021491",
                "expiry_date": 2016-12-31T00:00:00Z
            },
            {
                "uuid": "cf3a0fe014a2d",
                "printed_number": "Card 00084012",
                "expiry_date": 2015-12-31T00:00:00Z
            }
        ]
    }
]
```



## Data types

*Describe all datatypes used in this object*

### TokenPlainRfid *class*

Represents an plain RFID card as a token.

 Field Name      |  Field Type           |  Card.  |  Description
:----------------|:----------------------|:--------|:------------
 uuid            |  string(?)            |  1      |  UUID or _hidden id_ of the RFID card
 printed_number  |  string(150)          |  ?      |  Number printed on the card
 expiry_date     |  timestamp            |  1      |  Tokens may be used until the date of expiry is reached. To be handled by the partners systems. Expired roaming authorisations may be erased locally by each partner's systems.



### TokenXXXXX *class*

*Jet another token type, for extension*

 Field Name      |  Field Type           |  Card.  |  Description
:----------------|:----------------------|:--------|:------------
                 |                       |         | 


### GroupMode *enum*

| Value        | Description                                          |
| ------------ | ---------------------------------------------------- |
| ALL_EQUAL    | All tokens can be used interchangeable.              |
| OWN_SESSION  | Each token starts a own session, others can not access |
| ...          | **More examples? Needed?**                           |


### Features *enum*

| Value        | Description                                          |
| ------------ | ---------------------------------------------------- |
| AC_CHARGING  | Contract may charge at AC charge points              |
| DC_CHARGING  | Contract may charge at DC charge points              |
| ...          | **More examples? Needed?**                           |



