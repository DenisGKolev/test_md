FORMAT: 1A

# SkyArcher external protocol (external server)

This section describes the data which is forwarded to the external server via HTTP post requests by IPS

# Frames [/api/v1/dcs/add-frame]

## Receive frame [POST]

Receive a single frame from IPS server. No resend on fail

+ Request (text/plain)

	+ Attributes (object)
		+ DcmId: (number)
		+ DcsId: (string)
		+ Timestamp: (long)
		+ Frame: (byte[])

+ Response 200

# Descriptors [/api/v1/dcs/add-descriptors]

## Receive descriptors [POST]

Receive descriptors from IPS server. No resend on fail

+ Request (application/json)

    + Body

            {
                "Dcs":"some dcs id",
				"Descriptors" : [
				{
					"DcmId": 1,
					"ObjectId": "some object id",
					"Timestamp" : 20160824,
					"LocalTilt": 0.1,
					"LocalPan": 0.1,
					"DcmTilt": 0.1,
					"DcmPan": 0.1,
					"Age": 1,
					"AgeVisible": 1,
					"ConsecutiveInvisibleFrame": 1,
					"IsUav": true,
					"Uavity": 0.1,
					"ObjectState": "some state",
					"EstimatedSpeed": 0.1,
					"EstimatedSpeedX": 0.1,
					"EstimatedSpeedY": 0.1,
					"MassCentreX": 0.1,
					"MassCentreY": 0.1,
					"Latitude": 36.6,
					"Longtitude": 36.6,
					"BoundingBox": {
						"Top": 0.1,
						"Left": 0.1,
						"Width": 0.1,
						"Height": 0.1
					}
				}]
            }

    + Schema

            {
                "type": "object",
                "properties": {
                    "Dcs": {
                        "type": "string"
                    },
                    "Descriptors": {
                        "type": "array",
                        "items": {
                            "type": "object"
                        },
						"properties": {
							"DcmId": "number",
							"ObjectId": "string",
							"Timestamp" : "long",
							"LocalTilt": "double",
							"LocalPan": "double",
							"DcmTilt": "double",
							"DcmPan": "double",
							"Age": "number",
							"AgeVisible": "number",
							"ConsecutiveInvisibleFrame": "number",
							"IsUav": "boolean",
							"Uavity": "double",
							"ObjectState": "string",
							"EstimatedSpeed": "double",
							"EstimatedSpeedX": "double",
							"EstimatedSpeedY": "double",
							"MassCentreX": "double",
							"MassCentreY": "double",
							"Latitude": "double",
							"Longtitude": "double",
							"BoundingBox": {
								"type": "object",
								"properties": {
									"Top": "double",
									"Left": "double",
									"Width": "double",
									"Height": "double"
								}
							}
						}
                    }
                }
            }

+ Response 200


# SkyArcher subscription protocol (IPS server)

This section describes the requests sent by external server to the IPS

# Subscribe [/api/v1/external/subscribe]

## Subscribe for data [POST]

Subscribe on IPS. Start redirect

+ Request (text/plain)

	+ Attributes (object)
		+ URL: (string) external server url

+ Response 200

## Unsubscribe for data [POST]

Unsubscribe from IPS. Stop redirect

+ Request (text/plain)

	+ Attributes (object)
		+ URL: (string) external server url

+ Response 200
