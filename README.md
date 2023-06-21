Draft Contraflow Streets, Sydney
================================

This document is a draft that may become a blog post at https://jakecoppinger.com in future.

# Current streets allowing bicycle contraflow

(work in progress, incomplete list)
This is a map of the streets in the City of Sydney council area. The image is likely already out of date - click the link below to see the latest.

![](current-contraflow-22-06.png)


The query for this map is: https://overpass-turbo.eu/s/1wjm

```
[out:json][timeout:25];
(
  // Relation 1251066 is COS boundary:
  // https://www.openstreetmap.org/relation/1251066
  rel(1251066);map_to_area->.region;
  way["highway"]
  ["oneway:bicycle"="no"]
  (area.region);
);
out body;
>;
out skel qt;
```

# Street candidates that could make good contraflow streets
Work in progress. The following query finds roads in the City of Sydney that are:
- One way
- Do not currently allow bicycles to travel in the opposite direction
- Do not currently have a parallel separated cyelway

And excludes:
- Roads with more than 1 lane
- Dual carriageway one way roads
- Private roads
- Parking aisles, private or customer only roads
- Slip roads or highway links

![](possible-candidates-22-06.png)

Query: https://overpass-turbo.eu/s/1wlc

```
[out:json][timeout:25];
(
  // Relation 1251066 is COS boundary:
  // https://www.openstreetmap.org/relation/1251066
  rel(1251066);map_to_area->.region;
  
  // Select roads
  way["highway"]
  
  // Excluded under construction ways
  ["highway"!="construction"]
  // Excluded proposed ways
  ["highway"!="proposed"]
  
  // Only roads which are marked one way,
  // and don't allow bicycle contraflow
  ["oneway"="yes"]
  ["oneway:bicycle"!="no"]
  
  // Don't include roads that are bidirectional,
  // but are separated (and appear to be one way)
  ["dual_carriageway"!="yes"]
  
  // Don't include if a cycleway already present
  ["highway"!="cycleway"]
  
  // If a road is customers only it's likely
  // in a parking lot
  ["access"!="customers"]
  
  // Don't include roads where public access not allowed
  ["access"!="no"]
  
  // Don't include link roads (on ramps/slip roads)
  ["highway"!="motorway_link"]
  ["highway"!="primary_link"]
  ["highway"!="secondary_link"]
  ["highway"!="tertiary_link"]
  
  // Don't include major roads
  ["highway"!="primary"]
  ["highway"!="secondary"]
  
  
  ["lanes"!=2]
  ["lanes"!=3]
  ["lanes"!=4]
  ["lanes"!=5]
  ["lanes"!=6]
  ["access"!="private"]
  
  // Don't consider parking isles
  ["service"!="parking_aisle"]
  
  
  
  (area.region);
);
out body;
>;
out skel qt;
```

# List of streets from above that might be suitable for bicycle contraflow

## Terry Street, Surry Hills, 4.61m road width
- Laneway behind Metro Woolworths near central
- Would provide access from south Surry Hills to the Belmore Park cycleway (and further north into the city)
- Already marked as cycleroute on the official City of Sydney cycling map

## Sophia Street, Surry Hills, 4.9 metres width
- Long laneway with excellent visibility
- Gradient towards eastern end
- No parking, a number of infrequently used driveways
- Great link from Fitzroy St via Riley St to lower Surry Hills

## Lansdown Street, Surry Hills, ? width
- Car parking both sides
- Connects to Crown St
- Excellent visibility (completely straight)

## Boronia Lane, Surry Hills, ? width
- Already has contraflow marking, for pedestrians?
- Already close to Boronia Street though (allowing contraflow in last batch)
- Excellent visibility (completely straight)

## Davis Street, Surry Hills, ? width
- Connects to Bourke St cycleway
- Excellent visibility (completely straight)
- Car parking one side
- Has continuous footpath east side, west side is Crown St (future continuous footpath?)

## Rainford Street, Surry Hills, ? width
- Similar to Davis Street
- Excellent visibility (completely straight)
- Car parking one side
- Connects to Bourke St cycleway
- Has continuous footpath east side, west side is Crown St (future continuous footpath?)

## Emanuel Lane Sth of Cressy St, Roseberry, ? width
- Excellent visibility (completely straight)
- Alredy contraflow permitted Emanuel St north
- No car parking
- Similar design to Castlereagh Lane

## Blackwattle Lane, Ultimo, ? metres
- Already allows contraflow to north and south-east end

# Wynyard Lane, Sydney, ? metres
- The laneway just next to Wynyard Station
- Would provide a north -> south route for bikes avoiding York St, Carrington St buses and George St pedestrians

(work in progress, incomplete list)

# List of streets with potential issues
## High Holborn Street, Surry Hills
- Bend in road affecting visibility

## Bray Street, Newtown, ? metres (varies)
- Changes widths a number of times
- Existing traffic table + choker and traffic calming measures too narrow for bike + car (unsure if this is an issue)
- Parking both sides - 45 degree and parallel

# Wellington Street, Chippendale, ? metres
- Very narrow due to parking on one side

(work in progress, incomplete list)

# Lanes already near an existing contraflow or non-way-way lane

## Newman St, Newtown, ? metres
- Next lane north (Railway Lane) already one way (opposite) and suitable for bikes
- Car parking both sides so narrow in between
- Otherwise good charactistics:
  - Has modal filter at west end
  - Bicycle contraflow permitted & has paint at junction of Angel St

## Linthorpe St, Newtown, ? metres
- Nearby Wilson St contraflow lane

# Shephard Lane, Newtown, ? metres
- Near Ivy Street with contraflow

(work in progress, incomplete list)

# Additional maps

- All mapped streets with contraflow allowed (including outside City of Sydney): https://overpass-turbo.eu/s/1wjl

Query:
```
[out:json][timeout:25];
(
  way["highway"]
 
  ["oneway:bicycle"="no"]
  
  ({{bbox}});
);
out body;
>;
out skel qt;
```