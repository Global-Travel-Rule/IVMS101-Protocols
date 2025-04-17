# IVMS101 Standard

IVMS 101 provides a standard data model for transmitting required originator and beneficiary information. It is designed
for use primarily by VASPs, other obliged entities undertaking virtual asset services, and travel rule solution
providers.

Before continuing please review the document found here: [https://intervasp.org/](https://intervasp.org/)
Note: definitions for fields are described in the document.

IVMS provides a standard schema for data that represent VASPs and users on their respective platforms.

The standard represents each VASP and user as either Originator or Beneficiary.
For example:

```
{
  "originator": {},
  "beneficiary": {},
  "originatingVASP": {},
  "beneficiaryVASP": {}
}
```

In the case where your VASP is the exchange sending the crypto transaction (in the case of a withdrawal), your exchange
and your user is the originator. If your exchange is receiving the crypto transaction (in the case of a deposit), your
exchange and your user is the beneficiary.

Since both originating and beneficiary VASPs are entities, each object in the schema is represented by a legalPerson.
This object in the schema should include name, geographicAddress, nationalIdentification, customerIdentification.

Here is an example of an originating VASP.

```
"originatingVASP": {
    "legalPerson": {
      "name": {
        "nameIdentifier": [
          {
            "legalPersonName": "VASP A",
            "legalPersonNameIdentifierType": "LEGL"
          }
        ]
      },
      "geographicAddress": [
        {
          "addressType": "GEOG",
          "streetName": "Example Street",
          "buildingNumber": "123456",
          "buildingName": "Example Buinding",
          "postcode": "10110",
          "townName": "Test",
          "countrySubDivision": "TEST",
          "country": "US"
        }
      ],
      "nationalIdentification": {
        "nationalIdentifier": "123456789",
        "nationalIdentifierType": "LEIX"
      },
      "customerIdentification": "0x1234567890123456789012345678901234567890"
    }
  }
```

Note: customerIdentification in this case is the TrustAnchor Account.

Again, depending on whether you are the originating or beneficiary VASP, you are required to complete the appropriate
element in the schema:

```
{
  "originatingVASP": {},
  "beneficiaryVASP": {}
}
```

For users on your platform, they can be categorized as either naturalPerson or legalPerson depending on if they are an
individual or entity.

The following examples show an individual as the originator and entity as the beneficiary.

```
{
  "originator": {
    "originatorPersons": [
      {
        "naturalPerson": {
          "name": {
            "nameIdentifier": [
              {
                "primaryIdentifier": "Test",
                "secondaryIdentifier": "Test",
                "nameIdentifierType": "LEGL"
              }
            ]
          },
          "geographicAddress": [
            {
              "addressType": "GEOG",
              "streetName": "Example Street",
              "buildingNumber": "12345",
              "buildingName": "Test",
              "postcode": "10110",
              "townName": "Test Town",
              "countrySubDivision": "California",
              "country": "US"
            }
          ],
          "nationalIdentification": {
            "nationalIdentifier": "1234567",
            "nationalIdentifierType": "RAID",
            "countryOfIssue": "US",
            "registrationAuthority": "RA-TEST-123"
          },
          "customerIdentification": "0xAA13142141313242",
          "dateAndPlaceOfBirth": {
            "dateOfBirth": "1990-01-21",
            "placeOfBirth": "Test City"
          },
          "countryOfResidence": "US"
        }
      }
    ],
    "accountNumber": [
      "1HB5XM791313xHUJBsOP"
    ]
  }
}
```

```
{
    "beneficiary":
    {
        "beneficiaryPersons":
        [
            {
                "legalPerson":
                {
                    "name":
                    {
                        "nameIdentifier":
                        [
                            {
                                "legalPersonName": "Test Inc",
                                "legalPersonNameIdentifierType": "LEGL"
                            }
                        ]
                    },
                    "geographicAddress":
                    [
                        {
                            "addressType": "GEOG",
                            "streetName": "Test Street",
                            "buildingNumber": "123456",
                            "buildingName": "Test Building",
                            "postcode": "1222",
                            "townName": "Toronto",
                            "countrySubDivision": "Ontario",
                            "country": "CA"
                        }
                    ],
                    "nationalIdentification":
                    {
                        "nationalIdentifier": "012345678",
                        "nationalIdentifierType": "LEIX",
                        "countryOfIssue": "CA",
                        "registrationAuthority": "RA000589"
                    },
                    "customerIdentification": "0x3E21212121212CA",
                    "countryOfRegistration": "CA"
                }
            }
        ],
        "accountNumber":
        [
            "2XXXXXXXXXXXXXXXXXXXXXXXX"
        ]
    }
}
```

Note: the originator includes an accountNumber which is the withdrawal crypto address.

customerIdentification is the user id of the user in the attestation.

accountNumber for the beneficiary is the deposit address for the user on the beneficiary VASP.

The json schema validator that will confirm you have completed the json whether you are the originator
and beneficiary VASP prior to sharing the information with your counterparty.

It is important that you note how to translate your entity and users information into the schema accurately.

There are a number of open json schema validators that you can use to verify your json file validates against the
schema.

[https://jsonschema.dev/](https://jsonschema.dev/)

Provided here is the schema: json-schema.json

And an example of json: *-example.json