---
layout: home
sidebar:
  nav: sidemain
title: Occupancy
sort: 0
---
# Examples for Occupancy Information
## Introduction
When it comes to occupancy information, the APDS standard differentiates between 
* _Supply_ and
* _Demand_

The _Supply_ bit provides (semi-static) information about physically built parking capacity.  
The _Demand_ part provides (dynamic) information on occupied spaces.

## Supply
_Supply_ information can be provided from a `vehicleView` perspective, i.e. a calculated number of vehicles that can be fit into a parking area. Examples for this would be "pop-up parking on a green field" or on-street parking capacity in an area in a particular street (with no clear markings). As an alternative, the _Supply_ data can be specified from a `spaceView` perspective. This requires all spaces to be demarcated and identifiable. The latter view is the default.

Optionally, a validity information can be attached to _Supply_ data in order to communicate temporary changes in the capacity.

## Demand
_Demand_ information is typically collected in intervals. This update frequency may as well be of interest for readers of _Demand_ information.  
The provided data can relate to a single space or an area. The most popular use case is the latter, i.e. the occupancy of either a complete car park or an area within a car park (e.g. a level).

_Demand_ data can be specified in form of vehicle `count` information or a `percentage`. APDS also defines several ways of determining occupancy. This is communicated via the `occupancyCalculation` property(which can be one of

* `counted` (determination of a space being occupied via sensors and/or humans) 
* `derived` (the information is indirectly derived from other sources like e.g. payment data)
* `expected` (predictive information, e.g. based on historical data)
* `verified` (actively confirmed information)

Besides specifying the update interval (`frequency`), it is also important to timestamp collected occupancy information so the consumer knows how up-to-date it is. This is communicated via the `recordDateTime` property.

## Example
Time for an example. Let's assume a parking operator who runs a multi-storey car park downtown. The operator wants to connect to the city's parking guidance system. This municipal system is capable of actively retrieving occupancy information from connected, APDS-speaking systems. The operator exposes a corresponding endpoint (https://api.superpark.online/v4/parking/places) for the parking guidance system to continuously poll the car park system for occupancy information. The two parties also exchange some pre-shared information (car park id, API access credentials).

_Note: in this example, we do not elaborate on authentication and authorization related aspects_

### Occupancy Data Request
The parking guidance system reaches out to the operator's backend to retrieve occupancy information:

`GET https://api.superpark.online/v4/parking/places/CARPARK1?expand=occupancy`

The car park system responds with a payload like the one shown in the next paragraph.

### Occupancy Data Response

`HTTP/2 200`

```json5
{
    "id": "CARPARK1",
    "version": 1,
    "name": [
        {
            "language": "en",
            "string": "Piccadilly Place"
        }
    ],
    "hierarchyElementReference": {
        "elementId": {
            "id": "CARPARK1",
            "version": 1
        },
        "supply": [
            {
                "supplyViewType": "spaceView",
                "supplyQuantity": 220
            }
        ],
        "demandTable": [
            {
                "frequency": "PT3M",
                "timestamp": "2025-12-19T11:02:13Z",
                "demandType": [
                    {
                        "occupancyCalculation": "counted",
                        "count": 178,
                        "recordDateTime": "2025-12-19T11:01:57Z"
                    }
                ]
            }
        ]
    }
}
```

Let's take a look at the above payload. As you can see, it provides both, _Supply_ and _Demand_ information. 
* Via the `supply` list element, one can see that the car park consists of a total of 220 parking spaces.
* Via the `demandTable` element, two bits of information are being provided:
  * the info that occupancy data for this location will be updated in three minute increments
  * the most recent occupancy information showing 178 occupied spaces in the car park at 11:01 UTC (`recordDateTime` is when the information was counted, whereas the 11:02 `timestamp` property specifies when the car park system compiled this information)

### Interpretation
The city's parking now knows that it can expect to see an update frequency of 3 minutes for the data in question. They will configure their pull schedule accordingly. Together with information coming from other connected parking systems, the most recent occupancy information will then be displayed on VMSes installed throughout the city.

![VMS](/assets/images/usecases/VMSDisplay.png)

_Note:_ APDS provides a common data model for parking related information. It does however leave scope for implementation decisions. You may have noticed that the `demandType` element is an array. Theoretically, an implementor might decide to also provide (limited) historical data. For the above example use case however, one would probably rather only provide the most recent occupancy snapshot.