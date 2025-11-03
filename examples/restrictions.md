# Examples for Parking Restrictions
## No Parking
A parking location is not available for parking during the times specified in the Hrs Group, although there is no physical means of preventing parking at the location. Usually applies to on-street (though could also be used for a pay on arrival off street location where there is no facility for restricting access).

The following example shows the relevant part of a Place definition indicating __no parking__ between midnight and 6am:

```json
{
    "id": "PARKING_LOCATION_ID",
    "version": 1,

    "characteristics": {
        "accessControlled": false
    },

    "operatingRestrictions": [
        {
            "operatingRestriction": "noParking",
            "operatingRestrictionContext": [{ "language":"en", "string":"no parking from midnight till 6am"}],
            "times": {
                "validPeriods": [
                    {
                        "recurringTimePeriodOfDay": [
                            {
                                "startTimeOfPeriod": "00:00",
                                "endTimeOfPeriod": "06:00"
                            }
                        ],
                        "recurringDayWeekMonthPeriod": [
                            {
                                "applicableDay": [
                                    "monday",
                                    "tuesday",
                                    "wednesday",
                                    "thursday",
                                    "friday",
                                    "saturday",
                                    "sunday"
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Closed - no parking
A parking location is physically closed by a gate or other barrier during the times specified in the Hrs Group. Vehicles are not allowed to remain in the location when it is closed. Will apply to an off-street location. Vehicles remaining in the location during closed hours may be subject to a fine or other sanction and will not be retrievable, or retrieval will be charged for (the NPP will not provide details of sanctions)

The following example shows the relevant part of a Place definition indicating __closed: no parking__ between midnight and 6am:

```json
{
    "id": "PARKING_LOCATION_ID",
    "version": 1,

    "characteristics": {
        "accessControlled": true
    },

    "operatingRestrictions": [
        {
            "operatingRestriction": "noParking",
            "operatingRestrictionContext": [{ "language":"en", "string":"no parking from midnight till 6am"}],
            "times": {
                "validPeriods": [
                    {
                        "recurringTimePeriodOfDay": [
                            {
                                "startTimeOfPeriod": "00:00",
                                "endTimeOfPeriod": "06:00"
                            }
                        ]
                    }
                ]
            }
        }
    ],

    "times": {
        "operatingTime": {
            "validity": {
                "validityStatus": "definedByValidityTimeSpec",
                "validityTimeSpecification": {
                    "exceptionPeriods": [
                        {
                            "recurringTimePeriodOfDay": [
                                { 
                                    "startTimeOfPeriod": "00:00",
                                    "endTimeOfPeriod": "06:00"
                                }
                            ]
                        }
                    ]
                }
            }
        }
    }

}
```

The _accessControlled_ property indicates that there is is a barrier gate or other physical means to prevent parking. Parking is however not allowed between midnight and 6am as a corresponding _noParking_ operating restriction is effective during this period of time.


## Closed - no access
A parking location is physically closed by a gate or other barrier at the times specified in the Hrs Group. Vehicles are allowed to remain in the location when it is closed (subject to a tariff). Will apply to an off-street location. Vehicles entering before the location is closed may remain in the location during closed hours but will not be retrievable, or retrieval will be charged for during the closed hours (the NPP will not provide details of retrieval costs).

The following example shows the relevant part of a Place definition indicating __closed: no access__ between midnight and 6am:

```json
{
    "id": "PARKING_LOCATION_ID",
    "version": 1,

    "characteristics": {
        "accessControlled": true
    },

    "times": {
        "operatingTime": {
            "validity": {
                "validityStatus": "definedByValidityTimeSpec",
                "validityTimeSpecification": {
                    "exceptionPeriods": [
                        {
                            "recurringTimePeriodOfDay": [
                                { 
                                    "startTimeOfPeriod": "00:00",
                                    "endTimeOfPeriod": "06:00"
                                }
                            ]
                        }
                    ]
                }
            }
        }
    }

}
```

## Closed - exit only
A parking location is physically closed by a gate or other barrier preventing entry at the times specified in the Hrs Group. However, vehicles can exit the location during closed hours. Will apply to an off-street location. Vehicles entering before the location is closed may remain in the location during closed hours and can exit at any time.

The following example shows the relevant part of a Place definition indicating __closed - exit only__ between midnight and 6am:

```json
{
    "id": "PARKING_LOCATION_ID",
    "version": 1,

    "characteristics": {
        "accessControlled": true
    },

    "times": {
        "operatingTime": {
            "validity": {
                "validityStatus": "definedByValidityTimeSpec",
                "validityTimeSpecification": {
                    "exceptionPeriods": [
                        {
                            "recurringTimePeriodOfDay": [
                                { 
                                    "startTimeOfPeriod": "00:00",
                                    "endTimeOfPeriod": "06:00"
                                }
                            ]
                        }
                    ]
                }
            }
        },
        "accessAndEgress": [
            {
                "exitOpenTimeArea": [
                    {
                        "validityStatus": "definedByValidityTimeSpec",
                        "validityTimeSpecification": {
                            "validPeriods": [
                                {
                                    "recurringTimePeriodOfDay": [
                                        { 
                                            "startTimeOfPeriod": "00:00",
                                            "endTimeOfPeriod": "23:59"
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "entryOpenTimeArea": [
                    {
                        "validityStatus": "definedByValidityTimeSpec",
                        "validityTimeSpecification": {
                            "exceptionPeriods": [
                                {
                                    "recurringTimePeriodOfDay": [
                                        { 
                                            "startTimeOfPeriod": "00:00",
                                            "endTimeOfPeriod": "06:00"
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ]
            }
        ]
    }

}
```
The specified _exitOpenTimeArea_ indicates that it is possible to leave the parking location after hours.


## Unrestricted
There are no parking restrictions or tariff at the location during the times specified in the Hrs Group.
_(No need for an example as there simply will be no specification of any restrictions.)_



> per convention, gaps in the specification are interpreted as "unrestricted"



