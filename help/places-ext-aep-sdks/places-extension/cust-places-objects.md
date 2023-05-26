---
title: Egna platsobjekt
description: Information om anpassade inbyggda klasser som används med Places-API:er.
exl-id: deb16ba3-bd59-42b1-85ec-0f7de17f91f8
source-git-commit: 2f666081fa01c11e832b94c83f2fe2c66eb51766
workflow-type: tm+mt
source-wordcount: '38'
ht-degree: 5%

---

# Egna platsobjekt {#places-objects}

Här är de anpassade inbyggda klasserna som kommer att användas med Places-API:erna:

## iOS

### ACPlacesPoi

Här är definitionen:

```text
/**
 *  @class ACPPlacesPoi
 *
 *  This class contains data that is directly correlated to the properties maintained by the Places database.
 */
@interface ACPPlacesPoi : NSObject

@property (nonatomic, strong, nullable) NSString* identifier;  ///< The identifier for the POI
@property (nonatomic, strong, nullable) NSString* name;  ///< The name of the POI
@property (nonatomic) double latitude;  ///< The latitude of the POI's center
@property (nonatomic) double longitude;  ///< The longitude of the POI's center
@property (nonatomic) NSUInteger radius;  ///< The radius of the POI
@property (nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* metaData;  ///< Dictionary containing meta data for the POI
@property (nonatomic) Boolean userIsWithin;  ///< Indicates if the device is currently inside of this POI

@end
```

## Android

### PlatserPOI

```java
// only showing public methods available in the class
public class PlacesPOI {
    // returns the identifier for the POI
    public String getIdentifier();

    // returns the name for the POI
    public String getName();

    // returns whether the device is currently inside of this POI
    public boolean containsUser();

    // sets whether the device is currently inside of this POI
    public void setContainsUser(final boolean containsUser);

    // returns the latitude of the POI's center
    public double getLatitude();

    // returns the latitude of the POI's center
    public double getLongitude();

    // returns the radius of the POI
    public int getRadius();

    // returns map of meta data for the POI
    public Map<String, String> getMetadata();

    // returns the library to which this POI belongs
    public String getLibrary();
}
```
