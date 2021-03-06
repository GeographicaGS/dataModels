# Parking Spot

## Description

A parking spot is an area well delimited where *one* vehicle can be parked.
The aim of this entity type is to monitor the status of parking spots individually.
Thus, an entity of type `ParkingSpot` cannot exist without a containing entity of type
(`OnStreetParking`, `OffStreetParking`). A parking spot might belong to *one* group. 

## Data Model

+ `id` : Entity's unique identifier. 

+ `type` : Entity type. It must be equal to `ParkingSpot`.

+ `dateCreated` : Entity creation date.
    + Attribute type: [DateTime](https://schema.org/DateTime)
    + Optional

+ `dateModified` : Last update timestamp of this entity.
    + Attribute type: [DateTime](https://schema.org/DateTime)
    + Optional

+ `name` : Name of this parking spot. It can denote the number or label used to identify it within a parking site. 
    + Normative References: [https://schema.org/name](https://schema.org/name)
    + Optional

+ `description` : Description about the parking spot. 
    + Normative References: [https://schema.org/description](https://schema.org/description)
    + Optional

+ `location` : Geolocation of the parking spot, represented by a GeoJSON Point.
    + Attribute type: `geo:json`.
    + Normative References: [https://tools.ietf.org/html/rfc7946](https://tools.ietf.org/html/rfc7946)
    + Mandatory. Not nullable (if `address` is not defined).  
    
+ `address` : Registered parking spot civic address.
    + Normative References: [https://schema.org/address](https://schema.org/address)
    + Mandatory. Not nullable (if `location` is not defined).
    
+ `status` : Status of the parking spot from the point of view of occupancy.
    + Attribute type: [Text](https://schema.org/Text)
    + Allowed Values: one Of (`occupied`, `free`, `closed`, `unknown`)
    + Metadata:
        + `dateUpdated` : Timestamp which reflects the date when the attribute value was obtained. 
              + Type: [DateTime](https://schema.org/DateTime)
              + Optional
        + `TimeInstant` : [Timestamp](https://github.com/telefonicaid/iotagent-node-lib/blob/develop/README.md#TimeInstant)
        saved by FIWARE's IoT Agents. Note: This attribute has not been harmonized
to keep backwards compatibility with current FIWARE reference implementations. 
              + Type: [DateTime]((https://schema.org/DateTime). here can be production environmments where the attribute type
    is equal to the `ISO8601` string. If so, it must be considered as a synonym of `DateTime`.  
              + Optional
    + Mandatory

+ `width` : Width of the parking spot.
    + Attribute type: [Number](https://schema.org/Number)
    + Optional

+ `length` : Length of the parking spot.
    + Attribute type: [DateTime](https://schema.org/Number)
    + Optional

+ `refParkingGroup` : Group to which the parking spot belongs to. For model simplification purposes
only one group is allowed per parking spot. 
    + Attribute type: Reference to an entity of type `ParkingGroup`.  
    + Optional

+ `refParkingSite` : Parking site to which the the parking spot belongs to. 
    + Attribute type: Reference to an entity of type `OnStreetParking` or type `OffStreetParking`, depending on
    the value of the `category` attribute. 
    + Mandatory 

+ `category` : Category(ies) of the parking spot.
    + Attribute type: [Text](https://schema.org/Text)
    + Allowed values:
        + `onstreet`  : The parking spot belongs to an onstreet parking site.
        + `offstreet` : The parking spot belongs to an onstreet parking site.
        + Other values as per application needs
    + Mandatory
    
+ `TimeInstant` : [Timestamp](https://github.com/telefonicaid/iotagent-node-lib/blob/develop/README.md#TimeInstant)
saved by FIWARE's IoT Agent. Note: This attribute has not been harmonized
to keep backwards compatibility with current FIWARE reference implementations. 
    + Attribute type: [DateTime](https://schema.org/DateTime). There can be production environmments where the attribute type
    is equal to the `ISO8601` string. If so, it must be considered as a synonym of `DateTime`.  
    + Optional
    
+ `deviceId` : The device identifier (it could be the serial number) of the sensor used to monitor this parking spot.
    + Attribute type: [Text](https://schema.org/Text)
    + Optional

## Examples of use

    {
      "id": "santander:daoiz_velarde_1_5:3",
      "type": "ParkingSpot",
      "name": "A-13",
      "location": {
        "type": "Point",
        "coordinates": [-3.80356167695194, 43.46296641666926]
      },
      "status": "free",
      "category: ["onstreet"],
      "refParkingSite": "santander:daoiz_velarde_1_5"
    }

## Test it with a real service

## Open issues
