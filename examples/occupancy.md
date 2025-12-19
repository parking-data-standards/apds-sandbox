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

## Example 1
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

## Example 2: variation: reversal of communication relationship
After some time, the city (see [Example 1](#example-1)) introduces a new version of their parking guidance system. The key change is that, other than before, the system now expects connected car parks to pro-actively send their occupancy data updates to the city's backend. For this purpose, the city now exposes a corresponding APDS-speaking backend and exchanges the required details with all connected operators. From now on, operators are sending updates to the occupancy using a request like the following:

`PUT https://democity.parking-information.gov/v4/parking/places/CARPARK1` 

```json5
{    
    "id": "CARPARK1",
    "version": 1,
    "hierarchyElementReference": {
        "elementId": {
            "id": "CARPARK1",
            "version": 1
        },
        "demandTable": [
            {
                "frequency": "PT3M",
                "timestamp": "2025-12-21T17:12:13Z",
                "demandType": [
                    {
                        "occupancyCalculation": "counted",
                        "count": 114,
                        "recordDateTime": "2025-12-21T17:01:57Z"
                    }
                ]
            }
        ]
    }
}
```

## Example 3: less specific occupancy information
There is another city with many different car park operators. They all understand that the parking guidance system needs to provide input to motorists so they can make a qualified decision as to which car park to use. On the other hand - being competitors - the operators want to share as little information as possible in order to not provide too much insight into their commercial succcess. 

As a compromise solution, they agree upon less specific occupancy information to be provided that will still be good enough for drivers to make a decision.

### Solution: occupanyLevel
In the place hierarchy, APDS offers an element named `occupancyLevel` for this purpose. It holds a property `occupancyIndicator` which points to an entry of a user-defined code list.

#### Excursus: user-defined code lists
When implementing a system with a specific purpose in mind, there will always be situations where project-specific or application-specific aspects come into play. For this purpose, APDS offers the user-defined code lists mechanism. The general concept foresees that
* on the server side, a user-defined code list is provided via a corresponding URL
* on the client side, users can then reference entries from this list

A code list is uniquely identifiable (via its id and version) and has a list of possible values. These values can be agreed-upon between project partners.

#### User-defined code list for occupancy levels
The city defines the following code list for occupancy levels and offers it under a pre-shared URL (https://democity2.parking-information.gov/v4/parking/codelists/OCCUPANCYLEVEL):

```json5

{
    "id": "OCCUPANCYLEVEL",
    "version": 1,
    "locator": "https://democity2.parking-information.gov/v4/parking/codelists/OCCUPANCYLEVEL",
    "userDefinedCodeListEntries": [
        {
            "entryIndex": 0,
            "definedValue": "free",
            "entryDescription": "sufficient capacity available"
        },
        {
            "entryIndex": 1,
            "definedValue": "full",
            "entryDescription": "no more capacity available"
        },
        {
            "entryIndex": 2,
            "definedValue": "limited",
            "entryDescription": "limited capacity available"
        }
    ]
}
```

From now on, occupancy information can/must be provided by specifying one of the pre-defined values: `free`, `full`, `limited`.

#### Occupancy info via occupancyLevel
The car park operators now use these agreed-upon values to communicate occupancy information without disclosing too much detail. The following example shows one of the operators sending an update to the city's parking guidance system:

`PUT https://democity2.parking-information/v4/places/CARPARK1`

```json5
{
    "id": "CARPARK1",
    "version": 1,
    "occupancyLevel": {
        "occupancyIndicator": {
            "entryDefinedValue": "free"
        }
    }
}
```

#### Interpretation
The city decides to communicate the received information in form of a "traffic light" model

![VMS](/assets/images/usecases/VMSDisplay2.png)

