# Inventory Data Examples
Adopters who are new to the standard sometimes struggle starting with a "white sheet of paper". Here, concrete examples often can help. Below, you can find some real life examples created in collaboration with the "Fondation des Parkings".

## Dataset Contents
This minimal dataset contains details of two parking locations:

* P+R Étoile
* P+R Sécheron

Besides the core infrastructure specifics, tariff information is provided, too.

## APDS-formatted Representation

### Rate Table Data
an APDS-speaking data source would publish the tariff information as follows.

```json5
[
    {
        "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2",
        "version": 1,
        "rateTableName": [
            {
                "language": "ch", 
                "string": "Tarif P+R simplifié"
            }
        ],
        "availability": "public",
        "rateResponsibleParty": {
            "id": "FONDATION_DES_PARKINGS",
            "version": 1,
            "className": "Operator"
        },
        "rateLineCollections": [
            {
                "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2-0",
                "version": 1,
                "collectionSequence": 0,
                "applicableCurrency": "CHF",
                "minTime": "PT1H",
                "rateLines": [
                    {
                        "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2-0-0",
                        "version": 1,
                        "sequence": 0,
                        "description": [
                            {
                                "language": "fr",
                                "string": "par heure (7 premières heures)"
                            }
                        ],
                        "rateLineType": "flatRateTier",
                        "value": 3,
                        "durationStart": "00:00",
                        "durationEnd": "07:00",
                        "incrementPeriod": "PT1H",
                        "usageCondition": "unlimited",
                        "maxValue": 21
                    },
                    {
                        "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2-0-1",
                        "version": 1,
                        "sequence": 1,
                        "description": [
                            {
                                "language": "fr",
                                "string": "8 heures à une journée"
                            }
                        ],
                        "rateLineType": "flatRate",
                        "value": 3,
                        "durationStart": "00:00",
                        "durationEnd": "07:00",
                        "incrementPeriod": "PT5H",
                        "usageCondition": "once"                    }
                ]
            }
        ],
        "validity": {
            "validityStatus": "definedByValidityTimeSpec",
            "validityTimeSpecification": {
                "overallStartTime": "2026-01-01T00:00:01Z",
                "validPeriods": [
                    {
                        "periodName": [
                            {
                                "language": "fr",
                                "string": "Du lundi au vendredi de 7h à 19h"
                            }
                        ],
                        "recurringDayWeekMonthPeriod": [
                            {
                                "applicableDay": [ "monday", "tuesday", "wednesday", "thursday", "friday"]
                            }
                        ],
                        "recurringTimePeriodOfDay": [
                            {
                                "startTimeOfPeriod": "07:00",
                                "endTimeOfPeriod": "19:00"
                            }
                        ]
                    }
                ]
            }
        }
    }
]
```

### Place Data

```json5
[
    {
        "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
        "version": 1,
        "type": "place",
        "layer": 1,
        "name": [
            {
                "language": "fr",
                "string": "P+R Étoile"
            }
        ],
        "description": [
            {
                "language": "fr",
                "string": "<p>Parfaitement implanté dans le nouveau quartier d’affaires du PAV (Praille-Acacias-Vernets), au-dessus d’une autoroute urbaine et d’un axe de pénétration majeur de la ville, le P+R Etoile offre une connexion directe au centre-ville par le biais des lignes de tram, de bus, ainsi que de la halte Lancy-Pont-Rouge du Léman Express.</p><p>Il met à disposition des places de recharge pour les voitures électriques, ainsi que des emplacements pour personnes à mobilité réduite./p><p>Il dispose de places réservées aux véhicules d'auto-partage Mobility, d’une vélostation extérieure protégée et sécurisée et de nombreuses places pour les deux-roues motorisés.</p>"
            }
        ],
        "timeZone": "Europe/Zurich",
        "indicativePointLocation": {
            "type": "Point",
            "coordinates": [
                6.128169788,
                46.186960303
            ]
        },
        "placeStreetAddress": {
            "countryCode": "CH",
            "postCode": "1227",
            "city": [
                {
                    "language": "fr",
                    "string": "Carouge (GE)"
                }
            ],
            "addressLines": [
                {
                    "order": 0,
                    "type": "street",
                    "text": [
                        {
                            "language": "fr",
                            "string": "Carrefour de l'Étoile 1"
                        }
                    ]
                }
            ]
        },
        "characteristics": {
            "spacesTotal": 615,
            "openToPublic": true
        },
        "rightSpecifications": [
            {
                "id": "88d5835f-a957-42fc-b228-01bd4301fdee",
                "version": 1
            }            
        ]
        "responsibilityRoleAssignments": [
            {
                "type": "operator",
                "contactPoints": [
                    {
                        "id": "FONDATION_DES_PARKINGS",
                        "version": 1,
                        "organisationName": [
                            {
                                "language": "fr",
                                "string": "Fondation des parkings"
                            }
                        ],
                        "contactType": "contactPoint"
                    }
                ]
            }
        ]
    },
    {
        "id": "99d81ced-8390-4d29-9fe6-bbbdab067a29",
        "version": 1,
        "type": "identifiedArea",
        "accessType": "entry",
        "layer": 2,
        "name": [
            "language": "fr",
            "string": "Zone d'entrée"
        ],
        "parent":  {
            "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "indicativePointLocation": {
            "type": "Point",
            "coordinates": [
                6.12733,
                46.185688
            ]
        },
        "placeStreetAddress": {
            "countryCode": "CH",
            "postCode": "1212",
            "city": [
                {
                    "language": "fr",
                    "string": "Grand-Lancy (GE)"
                }
            ],
            "addressLines": [
                {
                    "order": 0,
                    "type": "street",
                    "text": [
                        {
                            "language": "fr",
                            "string": "Route des jeunes 6"
                        }
                    ]
                }
            ]
        }
    },
    {
        "id": "93a0d81e-3157-4c34-a0f7-a639f67ee342",
        "version": 1,
        "type": "identifiedArea",
        "layer": 2,
        "name": [
            {
                "language": "en",
                "string": "Parkings standard pour voitures"
            }
        ],
        "parent":  {
            "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 533
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "93a0d81e-3157-4c34-a0f7-a639f67ee342",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 533
                }
            ]
        }
    },
    {
        "id": "36dc833f-f41c-459e-a8f9-f9c7137efdfd",
        "version": 1,
        "type": "identifiedArea",
        "layer": 2,
        "name": [
            {
                "language": "en",
                "string": "Parkings avec possibilité de recharge"
            }
        ],
        "parent":  {
            "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 18
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "36dc833f-f41c-459e-a8f9-f9c7137efdfd",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 18
                }
            ]
        }
    },
    {
        "id": "6d93bf8b-b27d-4c2e-9b4f-8587f1d3c46d",
        "version": 1,
        "type": "identifiedArea",
        "layer": 2,
        "name": [
            {
                "language": "en",
                "string": "Parkings pour motos"
            }
        ],
        "parent":  {
            "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 64
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "6d93bf8b-b27d-4c2e-9b4f-8587f1d3c46d",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 64
                }
            ]
        }
    }

]
```

### Right Specification Data
In APDS, _Right Specifications_ define eligibility criteria for locations and tariffs.

```json5
[
    {
        "id": "88d5835f-a957-42fc-b228-01bd4301fdee",
        "version": 1,
        "type": "oneTimeUseParking",
        "hierarchyElements": [
            {
                "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
                "version": 1
            }
        ],
        "rateEligibility": [
            {
                "id": "88d5835f-a957-42fc-b228-01bd4301fdee-0",
                "version": 1,
                "rateTable": {
                    "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2",
                    "version": 1
                }
            }
        ],
        "issuer": {
            "id": "FONDATION_DES_PARKINGS",
            "version": 1,
            "className": "Operator"
        },
        "validity": {
            "validityStatus": "definedByValidityTimeSpec",
            "validityTimeSpecification": {
                "overallStartTime": "2026-01-01T00:00:01Z",
                "validPeriods": [
                    {
                        "periodName": [
                            {
                                "language": "fr",
                                "string": "Du lundi au vendredi de 7h à 19h"
                            }
                        ],
                        "recurringDayWeekMonthPeriod": [
                            {
                                "applicableDay": [ "monday", "tuesday", "wednesday", "thursday", "friday"]
                            }
                        ],
                        "recurringTimePeriodOfDay": [
                            {
                                "startTimeOfPeriod": "07:00",
                                "endTimeOfPeriod": "19:00"
                            }
                        ]
                    }
                ]
            }
        }
    }
]
```