# Examples engaging different RateLine Types

## flatRate
Example: vehicles are allowed to park up to 8 hours at a fixed price of &pound; 6.50.

_RateTable_
```json
{
	"id": "RATE_TABLE_ID",
	"version": 1,
	"rateTableName": [{ "language": "en", "string": "flat rate parking"}],
	"availability": "public",
	"rateType": "daily",
	"rateLineCollections": [
		{
			"collectionSequence": 0,
			"applicableCurrency": "GBP",
			"maxTime": "PT8H",
			"rateLines": [
				{
					"sequence": 0,
					"description": [{ "language": "en", "string": "fixed price for up to 8 hours"}],
					"rateLineType": "flatRate",
					"durationStart": "00:00",
					"durationEnd": "08:00",
					"incrementPeriod": "PT8H",
					"usageCondition": "once",
					"value": 6.5
				}
			]
		}
	],
	"validity": {
		"validityStatus": "definedByValidityTimeSpec",
        "validityTimeSpecification": {
            "overallStartTime": "2025-01-01T00:00:00Z",
            "validPeriods": [
				{
					"periodName": [{ "language": "en", "string": "Mon-Sun between 8am and 8pm"}],
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
					],
					"recurringTimePeriodOfDay": [
						{
							"startTimeOfPeriod": "08:00",
							"endTimeOfPeriod": "20:00"
						}
					]
				}
			]
	},
	"rateResponsibleParty": {
		"id": "TESTCOUNCIL",
		"version": 1,
		"className": "Operator"
	}
}
```

_RightSpecification_
```json
{
	"id": "RIGHT_SPEC_ID",
	"version": 1,
	"type": "oneTimeUseParking",
	"rateEligibility": [
		{
			"id": "ELIGIBILITY_1",
			"version": 1,
			"rateTable": { "id": "RATE_TABLE_ID", "version": 1}
		}
	],
	"validity": {
		"validityStatus": "active"
	},
	"rateTransition": {
		"overpaymentPolicy": "rateEndCutOff",
		"followThroughAllowed": false,
		"prepaymentAllowed": false,
		"reservationAvailable": false
	}
}
```


## flatRateTier
Example: a parking operator posts the following tariff:  
* first half hour: &pound; 3
* second half hour: &pound; 2
* any subsequent hour: &pound; 1
* max. stay: 7 hours

_RateTable_
```json
{
	"id": "RATE_TABLE_ID",
	"version": 1,
	"rateTableName": [{ "language": "en", "string": "standard day on-street"}],
	"availability": "public",
	"rateType": "hourly",
	"rateLineCollections": [
		{
			"collectionSequence": 0,
			"applicableCurrency": "GBP",
			"maxTime": "PT7H",
			"rateLines": [
				{
					"sequence": 0,
					"description": [{ "language": "en", "string": "up to 30 minutes"}],
					"rateLineType": "flatRateTier",
					"durationStart": "00:00",
					"durationEnd": "00:30",
					"incrementPeriod": "PT30M",
					"value": 3,
					"usageCondition": "once"
				},
				{
					"sequence": 1,
					"description": [{ "language": "en", "string": "up to 1 hour"}],
					"rateLineType": "flatRateTier",
					"durationStart": "00:30",
					"durationEnd": "01:00",
					"incrementPeriod": "PT30M",
					"value": 2,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "up to 2 hours"}],
					"rateLineType": "flatRateTier",
					"durationStart": "01:00",
					"durationEnd": "02:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "up to 3 hours"}],
					"rateLineType": "flatRateTier",
					"durationStart": "02:00",
					"durationEnd": "03:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "up to 4 hours"}],
					"rateLineType": "flatRateTier",
					"durationStart": "03:00",
					"durationEnd": "04:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "up to 5 hours"}],
					"rateLineType": "flatRateTier",
					"durationStart": "04:00",
					"durationEnd": "05:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "up to 6 hours"}],
					"rateLineType": "flatRateTier",
					"durationStart": "05:00",
					"durationEnd": "06:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "up to 7 hours"}],
					"rateLineType": "flatRateTier",
					"durationStart": "06:00",
					"durationEnd": "07:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "once"
				}
			]
		}
	]
}
```



## incrementingRate
Example: parking costs &pound; 1.50 per half hour up to a maximum of &pound; 7.50.

_RateTable_
```json
{
	"id": "RATE_TABLE_ID",
	"version": 1,
	"rateTableName": [{ "language": "en", "string": "(half-) hourly parking"}],
	"availability": "public",
	"rateType": "hourly",
	"rateLineCollections": [
		{
			"collectionSequence": 0,
			"applicableCurrency": "GBP",
			"rateLines": [
				{
					"sequence": 0,
					"description": [{ "language": "en", "string": "per 30 minutes"}],
					"rateLineType": "incrementingRate",
					"durationStartTime": "00:00",
					"durationEndTime": "15:00",
					"incrementPeriod": "PT30M",
					"value": 1.5,
					"maxValue": 7.5,
					"usageCondition": "unlimited"
				}
			]
		}
	],
	"validity": {
		"validityStatus": "definedByValidityTimeSpec",
        "validityTimeSpecification": {
            "overallStartTime": "2025-01-01T00:00:00Z",
            "validPeriods": [
				{
					"periodName": [{ "language": "en", "string": "Mon-Sun between 7am and 10pm"}],
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
					],
					"recurringTimePeriodOfDay": [
						{
							"startTimeOfPeriod": "07:00",
							"endTimeOfPeriod": "22:00"
						}
					]
				}
			]
	},
	"rateResponsibleParty": {
		"id": "TESTCOUNCIL",
		"version": 1,
		"className": "Operator"
	}
}
```

_RightSpecification_
```json
{
	"id": "RIGHT_SPEC_ID",
	"version": 1,
	"type": "oneTimeUseParking",
	"rateEligibility": [
		{
			"id": "ELIGIBILITY_1",
			"version": 1,
			"rateTable": { "id": "RATE_TABLE_ID", "version": 1}
		}
	],
	"validity": {
		"validityStatus": "active"
	},
	"rateTransition": {
		"overpaymentPolicy": "rateEndCutOff",
		"followThroughAllowed": false,
		"prepaymentAllowed": false,
		"reservationAvailable": false
	}
}
```


## Combinations
The _flatRateTier_ example can also be represented in an abbreviated form using a combination of _flatRateTier_ and _incrementingRate_ rate lines like this:  

_RateTable_
```json
{
	"id": "RATE_TABLE_ID",
	"version": 1,
	"rateTableName": [{ "language": "en", "string": "standard day on-street"}],
	"availability": "public",
	"rateType": "hourly",
	"rateLineCollections": [
		{
			"collectionSequence": 0,
			"applicableCurrency": "GBP",
			"maxTime": "PT7H",
			"rateLines": [
				{
					"sequence": 0,
					"description": [{ "language": "en", "string": "up to 30 minutes"}],
					"rateLineType": "flatRateTier",
					"durationStart": "00:00",
					"durationEnd": "00:30",
					"incrementPeriod": "PT30M",
					"value": 3,
					"usageCondition": "once"
				},
				{
					"sequence": 1,
					"description": [{ "language": "en", "string": "up to 1 hour"}],
					"rateLineType": "flatRateTier",
					"durationStart": "00:30",
					"durationEnd": "01:00",
					"incrementPeriod": "PT30M",
					"value": 2,
					"usageCondition": "once"
				},
				{
					"sequence": 2,
					"description": [{ "language": "en", "string": "1-7 hours"}],
					"rateLineType": "incrementingRate",
					"durationStart": "01:00",
					"durationEnd": "07:00",
					"incrementPeriod": "PT1H",
					"value": 1,
					"usageCondition": "unlimited"
				}
			]
		}
	]
}
```
