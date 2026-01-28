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

{
    "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2",
    "version": 1,
    "rateTableName": [
        {
            "language": "ch", 
            "string": "Tarif P+R Étoile"
        }
    ],
    "availability": "public",
	"additionalInformation": "https://www.geneve-parking.ch/fr/ou-stationner/pr-etoile",
    "rateResponsibleParty": {
        "id": "FONDATION_DES_PARKINGS",
        "version": 1,
        "className": "Operator"
    }
}

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
            ],
            "demandTable": [
                {
                    "frequency": "PT3M",
                    "timestamp": "2026-01-26T17:02:00Z",
                    "demandType": [
                        {
                            "occupancyCalculation": "counted",
                            "count": 500,
                            "recordDateTime": "2026-01-26T17:01:23Z"
                        }
                    ]
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
            ],
            "demandTable": [
                {
                    "frequency": "PT3M",
                    "timestamp": "2026-01-26T17:02:00Z",
                    "demandType": [
                        {
                            "occupancyCalculation": "counted",
                            "count": 16,
                            "recordDateTime": "2026-01-26T17:01:23Z"
                        }
                    ]
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
            ],
            "demandTable": [
                {
                    "frequency": "PT3M",
                    "timestamp": "2026-01-26T17:02:00Z",
                    "demandType": [
                        {
                            "occupancyCalculation": "counted",
                            "count": 50,
                            "recordDateTime": "2026-01-26T17:01:23Z"
                        }
                    ]
                }
            ]
        }
    }

]
```

The above payload creates a part of what _APDS_ calls a _Place Hieararchy_. In the example, we now have a car park with three _Identified Area_s as children plus a fourth _Identified Area_ describing the main entry area:

![Hierarchy](/assets/images/usecases/hierarchy.png)

### Right Specification Data
In APDS, _Right Specifications_ define eligibility criteria for locations and tariffs, i.e. they "tie" the _Rate Table_ to the _Place_ (including potential conditions).  
That way, it would e.g. be possible to offer a (more expensive) standard tariff and a reduced tariff for electric vehicles.

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

## 2nd Dataset
The second parking location (P+R Sécheron) is similarly structured.

### Rate Table
Here is the _APDS_ representation of the P+R Sécheron tariff:

```json5

{
    "id": "006a3d45-eee1-44eb-9e53-ce4163359d9f",
    "version": 1,
    "rateTableName": [
        {
            "language": "ch", 
            "string": "Tarif P+R Sécheron"
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
            "id": "006a3d45-eee1-44eb-9e53-ce4163359d9f-0",
            "version": 1,
            "collectionSequence": 0,
            "applicableCurrency": "CHF",
            "minTime": "PT1H",
            "rateLines": [
                {
                    "id": "006a3d45-eee1-44eb-9e53-ce4163359d9f-0-0",
                    "version": 1,
                    "sequence": 0,
                    "description": [
                        {
                            "language": "fr",
                            "string": "par heure (10 premières heures)"
                        }
                    ],
                    "rateLineType": "flatRateTier",
                    "value": 2,
                    "durationStart": "00:00",
                    "durationEnd": "10:00",
                    "incrementPeriod": "PT1H",
                    "usageCondition": "unlimited",
                    "maxValue": 20
                },
                {
                    "id": "79ab1c25-289f-4a6c-b6b3-682ba1dea0e2-0-1",
                    "version": 1,
                    "sequence": 1,
                    "description": [
                        {
                            "language": "fr",
                            "string": "11 heures à une journée"
                        }
                    ],
                    "rateLineType": "flatRate",
                    "value": 1,
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

```


### Place Data

```json5
[
    {
        "id": "34a71857-1fd0-4eac-82e4-4ff8c8700ffa",
        "version": 1
        "type": "place",
        "layer": 1,
        "name": [
            {
                "language": "fr",
                "string": "P+R Sécheron"
            }
        ],
        "timeZone": "Europe/Zurich",
        "indicativePointLocation": {
            "type": "Point",
            "coordinates": [
                6.145382384,
                46.220735699
            ]
        },
        "placeStreetAddress": {
            "countryCode": "CH",
            "postCode": "1202",
            "city": [
                {
                    "language": "fr",
                    "string": "Genève (GE)"
                }
            ],
            "addressLines": [
                {
                    "order": 0,
                    "type": "street",
                    "text": [
                        {
                            "language": "fr",
                            "string": "Rue Kazem-RADJAVI 8"
                        }
                    ]
                }
            ]
        },
        "characteristics": {
            "spacesTotal": 523,
            "openToPublic": true
        },
        "rightSpecifications": [
            {
                "id": "32d7f4b1-fcf2-467f-b536-b77aef90372e",
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
        ],
        "operatingRestrictions": [
            {
                "operatingRestriction": "noParking",
                "operatingRestrictionContext": [{ "language":"en", "string":"Fermé de 19h à 7h"}],
                "times": {
                    "validPeriods": [
                        {
                            "recurringTimePeriodOfDay": [
                                {
                                    "startTimeOfPeriod": "19:00",
                                    "endTimeOfPeriod": "07:00"
                                }
                            ],
                            "recurringDayWeekMonthPeriod": [
                                {
                                    "applicableDay": [
                                        "monday",
                                        "tuesday",
                                        "wednesday",
                                        "thursday",
                                        "friday"
                                    ]
                                }
                            ]
                        }
                    ]
                }
            }
        ]        
    },
    {
        "id": "a07c59ba-31fb-4f08-a79d-8629bbda8174",
        "version": 1,
        "type": "identifiedArea",
        "accessType": "entry",
        "layer": 2,
        "name": [
            "language": "fr",
            "string": "Zone d'entrée"
        ],
        "parent":  {
            "id": "34a71857-1fd0-4eac-82e4-4ff8c8700ffa",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "indicativePointLocation": {
            "type": "Point",
            "coordinates": [
                6.1455893577004,
                46.221146070017
            ]
        },
        "placeStreetAddress": {
            "countryCode": "CH",
            "postCode": "1202",
            "city": [
                {
                    "language": "fr",
                    "string": "Genève (GE)"
                }
            ],
            "addressLines": [
                {
                    "order": 0,
                    "type": "street",
                    "text": [
                        {
                            "language": "fr",
                            "string": "Rue Kazem-RADJAVI 8"
                        }
                    ]
                }
            ]
        }
    },
    {
        "id": "9035fdeb-8574-4ebd-b42a-64007a33d67d",
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
            "id": "34a71857-1fd0-4eac-82e4-4ff8c8700ffa",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 406
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "9035fdeb-8574-4ebd-b42a-64007a33d67d",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 406
                }
            ]
        }
    },
    {
        "id": "8d7da1ec-c9ab-4284-9ef3-86e88a3be9dc",
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
            "id": "34a71857-1fd0-4eac-82e4-4ff8c8700ffa",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 18
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "8d7da1ec-c9ab-4284-9ef3-86e88a3be9dc",
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
        "id": "9e9efb82-2e6e-4171-8aa2-786802f3c894",
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
            "spacesTotal": 44
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "9e9efb82-2e6e-4171-8aa2-786802f3c894",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 44
                }
            ]
        }
    },
    {
        "id": "5dad87f3-5707-4c63-94f0-8dbe5ce9fb57",
        "version": 1,
        "type": "identifiedArea",
        "layer": 2,
        "name": [
            {
                "language": "en",
                "string": "Parkings pour vélos"
            }
        ],
        "parent":  {
            "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 55
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "5dad87f3-5707-4c63-94f0-8dbe5ce9fb57",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 55
                }
            ]
        }
    },
    {
        "id": "bfaf2341-145c-47fd-acf4-8b8c985037e8",
        "version": 1,
        "type": "identifiedArea",
        "layer": 2,
        "name": [
            {
                "language": "en",
                "string": "Personnes à mobilité réduite"
            }
        ],
        "parent":  {
            "id": "f4fdae01-929f-47d5-aeaa-4e5d138a83c0",
            "version": 1,
        },
        "timeZone": "Europe/Zurich",
        "characteristics": {
            "spacesTotal": 5
        },
        "hierarchyElementReference": {
            "elementId": {
                "id": "bfaf2341-145c-47fd-acf4-8b8c985037e8",
                "version": 1,
            },
            "supply": [
                {
                    "supplyViewType": "spaceView",
                    "supplyQuantity": 5
                }
            ]
        }
    }

]
```

Please take note of the specified operating restrictions indicating when the parking is closed and doesn't allow vehicles to be parked there.

### Right Specification Data
Like you already saw in the first example, one (or more) _Right Specification_s define who is eligible for which tariff and when. Here is the corresponding spec for P+R Sécheron:

```json5
[
    {
        "id": "32d7f4b1-fcf2-467f-b536-b77aef90372e",
        "version": 1,
        "type": "oneTimeUseParking",
        "hierarchyElements": [
            {
                "id": "34a71857-1fd0-4eac-82e4-4ff8c8700ffa",
                "version": 1
            }
        ],
        "rateEligibility": [
            {
                "id": "32d7f4b1-fcf2-467f-b536-b77aef90372e-0",
                "version": 1,
                "rateTable": {
                    "id": "006a3d45-eee1-44eb-9e53-ce4163359d9f",
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

