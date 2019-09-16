# Required Inputs
The following values must be sent in the request.  If any of these values are missing or cannot be cast to the correct data type, LoopLink<sup>&reg;</sup> GSE will return an error.

## Location

> **Status:** **DEPRECATED IN V2**

> **Name:** `location`

> **Type:** String

> **Description:** Text string that can be geocoded to a latitude and longitude.

> **Accepts:**
>> * Complete address (1234 Road Name St., Brookings SD 57006)
* ZIP/Postal code (57006) SEE NOTES
* City, State/Province pair (Brookings, South Dakota)


> **Notes:**
>> LoopLink<sup>&reg;</sup> GSE is designed to attempt to respond successfully regardless of the location search. Inputs like 'the mall' may return a location but that location may not have anything to do with the user's actual location.

>> When using Zip/Postal Code searches, you should include a Country in order to increase the accuracy of the search especially if your target user is outside of the United States. The bulk of searches through the service originate in the U.S. so, LoopLink<sup>&reg;</sup> GSE will automatically default Zip/Postal code searches that match the same pattern as a U.S. zip code to the United States of America.

## Street

> **Name:** `street`

> **Type:** String

> **Description:** Text string indicating the street address with house/building number for the location address.

> **Accepts:**
>> * Street address 1234 Road Name St.

## City

> **Name:** `city`

> **Type:** String

> **Description:** Text string indicating the city or town for the location address.

> **Accepts:**
>> * Name of city, town village, hamlet, borough etc.

## State

> **Name:** `state`

> **Type:** String

> **Description:** Text string indicating the state or province for the location address.

> **Accepts:**
>> * Name of state, province or local geographic equivalent.

## ZIP/Postal Code

> **Name:** `postal_code`

> **Type:** String

> **Description:** Text string indicating the postal code for the location address.

> **Accepts:**
>> * Postal code for the location address.

> **Notes:**
>> If searching with only a Zip/Postal Code you muse include a Country in the request. LoopLink<sup>&reg;</sup> GSE checks if postal codes match the same pattern as a U.S. zip code and if so will append United States of America to the country automatically prior to search.

## Country

> **Name:** `country`

> **Type:** String

> **Description:** Text string indicating the country for the location address.

> **Accepts:**
>> * Name, ISO Alpha-2 or ISO Alpha-3 Code of the search location's country.

### Geo-Coded Location Requests
It is possible to directly enter a location by signed latitude and longitude. When doing so, you must specify the request is geocoded using a `geocoded` field set to True. Additionally, your request should not include `location` it should instead include `lat` and `lon`.

> **Status:** **DEPRECATED IN V2** Inclusion will not cause an error but the value will be ignored.

> **Name:** `geocoded`

> **Type:** Boolean

> **Description:** Indicates to the server that you are providing `lat` and `lon` instead of `location`

> **Default:** false

> **Accepts:**
>> - True (String or Integer):  true or a non-zero integer
- False(String or Integer): false or 0

> **Name:** `lat`

> **Type:** String or Float

> **Description:** Signed latitude in degrees format

> **Accepts:** Any float or string representation of a number between -90 and +90

> **Name:** `lon`

> **Type:** String or Float

> **Description:** Signed longitude in degrees format

> **Accepts:** Any float or string representation of a number between -180 and +180

## Above Grade Area

> **Name:** `above_grade_area`

> **Type:** Float

> **Description:** Area of conditioned space above grade.

> **Units:**
>> - **IP:** Square Feet
- **SI:** Square Meters

> **Accepts:** Any number greater than zero

> **Example:** A 100' square home with two stories and basement would have 2\*100\*100 = 20,000sqft of above grade square footage.

> **Notes:** While it is possible to enter a zero value for above grade area, the sum of above grade area and below grade area must be greater than zero to avoid an error.

## Below Grade Area
> **Name:** `below_grade_area`

> **Type:** Float

> **Description:** Area of conditioned space below grade.

> **Units:**
>> - **IP:** Square Feet
- **SI:** Square Meters

> **Accepts:** Any number greater than zero

> **Example:** A 100' square home with two stories and basement would have 1\*100\*100 = 10,000sqft of below grade square footage.

> **Notes:** While it is possible to enter a zero value for below grade area, the sum of above grade area and below grade area must be greater than zero to avoid an error.

## Age of Home
> **Name:** `age_home`

> **Type:** Integer

> **Description:** Number of years since the home was built. The age of the home is used in calculating unspecified building construction details as well as estimating degradation of equipment performance over time.


## HVAC Comparative Heating Technology
> **Name:** `heating_comp`

> **Type:** String

> **Description:** Name of the traditional heating system against which we are running a cost comparison.

> **Accepts:**
>> - natural gas
- eletric resistance
- propane
- fuel oil
- ashp
- none (false)

> **Notes:** It is recommended that this field be presented as a drop down menu as the accepted values must exactly match those listed.

> If set to 'none' or false, the heating portion of the savings calculation will be ignored.

## Hot Water Comparative Technology
> **Name:** `hwg_comp`

> **Type:** String

> **Description:** Name of the traditional domestic hot water generation system against which we are running a cost comparison. This type of system will also be used in supplemental estimations if the percent of hotwater generated by geothermal is less than 100%.

> **Accepts:**
>> - natural gas
- eletric resistance
- propane
- fuel oil
- none (false)

> **Notes:** It is recommended that this field be presented as a drop down menu as the accepted values must exactly match those listed.

> If set to 'none' or false, the hot water portion of the savings calculation will be ignored.

# Optional Inputs
Optional fields default to standard values but will accept user inputs to further refine savings estimation. It is not necessary to give end users access to these variables. However, it is recommended for certain values like utility rates that are difficult to accurately estimate for all locations.

## Use SI Units

> **Name:** `use_si`

> **Type:** Boolean

> **Description:** Flags the system to accept SI inputs and outputs. The values will be converted on the server into IP units before and after processing. This means that the user's inputs are susceptible to some minor rounding errors when returned.

> **Default:** false

> **Accepts:**
>> - True (String or Integer):  true or a non-zero integer
- False(String or Integer): false or 0

## GSHP Is Variable Speed

> **Name:** `is_variable`

> **Type:** Boolean

> **Description:** Adjusts the estimated performance and efficiency of the GSHP system.

> **Default:** false

> **Accepts:**
>> - True (String or Integer):  true or a non-zero integer
- False(String or Integer): false or 0

## Ignore Cooling

> **Name:** `ignore_cooling`

> **Default:** false

> **Description:** Ignore cooling in estimate. An empty value will be treated as False.

> **Accepts:**
>> - True (String or Integer):  true or a non-zero integer
- False(String or Integer): false or 0

## Heating Set Point Temperature

> **Name:** `set_point_heating`

> **Default:** 70 &deg;F

> **Description:** Desired indoor air temperature in heating months.

> **Units:**  &deg;F (&deg;C)

> **Accepts:**  60&deg;F <= set_point_heating <= 90&deg;F

## Cooling Set Point Temperature

> **Name:** `set_point_cooling`

> **Type:** Integer

> **Description:** Desired indoor air temperature in cooling months.

> **Default:** 75&deg;F

> **Units:**  &deg;F (&deg;C)

> **Accepts:** 60&deg;F <= set_point_cooling <= 90&deg;F

## Heating System Age
> **Name:** `age_heating_comp`

> **Type:** Integer

> **Description:** Describes the age of the comparative heating system

> **Default:** age_home

> **Accepts:** >= 0

## Cooling System Age
> **Name:** `age_cooling_comp`

> **Type:** Integer

> **Description:** Describes the age of the comparative cooling system

> **Default:** age_home

> **Accepts:**  >= 0

## Number of Residents
> **Name:** `num_residents`

> **Type:** Integer

> **Description:** Number of people living in space year round

> **Default:** 4

> **Accepts:**  1 <= num_residents <= 20

## Hot Water System Age
> **Name:** `age_hwg`

> **Type:** Integer

> **Description:** Describes the age of the comparative hot water system

> **Default:** age_home

> **Accepts:**  >= 0

## Hot Water Supply Temp
> **Name:** `supply_temp_hwg`

> **Type:** Integer

> **Description:** Desired hot water temperature

> **Default:** varies by location

> **Units:**  &deg;F (&deg;C)

> **Accepts:**  33&deg;F <= supply_temp_hwg <= 90&deg;F

## Hot Water Set Point
> **Name:** `set_point_hwg`

> **Type:** Integer

> **Description:** Desired hot water temperature

> **Default:** 120&deg;F

> **Units:**  &deg;F (&deg;C)

> **Accepts:** hwg_supply_temp < set_point_hwg <= 145&deg;F

## Hot Water From Geo Annual
> **Name:** `annual_percent_geo_hwg`

> **Type:** Integer

> **Description:** Percentage of total hot water generated by geo

> **Default:** 100

> **Accepts:** 0  <= annual_percent_geo_hwg <= 100

## Hot Water Standing Losses
> **Name:** `standing_losses_hwg`

> **Type:** Integer

> **Description:** Percentage of heat energy lost while storing hot water

> **Default:** 10%

> **Accepts:**  0% <= standing_losses_hwg <= 100%

## Hot Water Volume Per Resident
> **Name:** `vol_per_res_hwg`

> **Type:** Integer

> **Description:** Volume of hot water consumed per day by each resident

> **Default:** 20gal

> **Units:**  US Gallons (Liters)

> **Accepts:** 0 <= vol_per_res_hwg <= 150gal

## Ventilation CFM
> **Name:** `ventilation_cfm`

> **Type:** float

> **Description:** Ventilaton airflow rate to include in the load estimate calculation 

> **Default:** 0

> **Units:**
>> - **IP:** Cubic feet per minute (cfm)
- **SI:** Cubic meters per hour

> **Accepts:** Any number greater than zero

## Ventilation Energy Recovery Effectiveness
> **Name:** `ventilation_eff`

> **Type:** float

> **Description:** The energy recovery effectiveness of the ERV/HRV fresh air ventilation system (expressed as a decimal)

> **Default:** 0

> **Accepts:** Any number between 0 and 1.

## Average Above Grade Ceiling Height

> **Name:** `avg_above_grade_ceiling_height`

> **Type:** Float

> **Description:** Average ceiling height of above grade conditioned space.

> **Default:** 8.0 ft

> **Units:**
>> - **IP:** Feet
- **SI:** Meters

> **Accepts:** Any number greater than zero

> **Example:** A home with two stories above grade with equal area. The first floor has an average ceiling height of 10 ft and the second floor has an average ceiling height of 8 ft = (8+10)/2 = 9 ft average ceiling height.

## Above Grade Floors

> **Name:** `above_grade_floors`

> **Type:** Float

> **Description:** The number of above grade floors/stories in the home.

> **Default:** 1.5

> **Accepts:** Any number greater than one

## Basement
> **Name:** `basement`

> **Type:** String

> **Description:** Describes the basement

> **Default:** conditioned unless below_grade_area == 0 in which case default is slab

> **Accepts:**
>> - conditioned
- unconditioned
- slab

## Basement Insulation
> **Name:** `basement_insulation`

> **Type:** String

> **Description:** Allows peak load calculation adjustment for uninsulated but conditioned basement type

> **Default:** insulated

> **Accepts:**
>> - insulated
- uninsulated

> **Notes:** This input will only impact the load calculations for 'conditioned' basement type.

## Below Grade Depth
> **Name:** `below_grade_depth`

> **Type:** Float

> **Description:** Average below grade of basement walls.

> **Default:** 8.0 ft

> **Units:**
>> - **IP:** Feet
- **SI:** Meters

> **Accepts:** Any number greater than zero

> **Example:** A walkout basement with 1/2 of the walls 8 ft below grade and 1/2 of the walls 4 ft below grade will have (8+4)/2 = 6 ft average below grade depth.

> **Notes:** This input will only impact the load calculations for 'conditioned' basement type.

## Insulation Level
> **Name:** `insulation_level`

> **Type:** String

> **Description:** Describes the insulation used in the home

> **Default:** good

> **Accepts:**
>> - poor (Brick Walls w/ No Insulation, R-10 Ceiling Insulation)
- ok  (R-11 walls, R-19 ceilings)
- good (R-19 walls, R-30 ceilings)
- excellent (R-30 walls, R-38 ceilings)

## Building Tightness
> **Name:** `building_tightness`

> **Type:** String

> **Description:** Describes the resistance to infiltration of the structure.

> **Default:** Varies by age of home

> **Accepts:**
>> - loose
- semi-loose
- average
-semi-tight
- tight

## Ductwork Placement
> **Name:** `duct_place`

> **Type:** String

> **Description:** Describes where in the building ductwork is installed.

> **Default:** conditioned unless below_grade_area == 0 in which case default is unconditioned attic

> **Accepts:**
>> - conditioned
- unconditioned basement
- unconditioned_basement_leaky
- unconditioned attic

## Ductwork Sealing
> **Name:** `duct_seal`

> **Type:** String

> **Description:** Describes amount of air/energy lost through duct fittings and connections.

> **Default:** average

> **Accepts:**
>> - unsealed
- partial
- average
- notable
- extreme

## Ductwork Insulation
> **Name:** `duct_insulation`

> **Type:** String

> **Description:** Describes how well insulated ducts are from transmission loss.

> **Default:** R6

> **Accepts:**
>> - R0
- R2
- R4
- R6
- R8

## Utility Rates

The system will by default attempt to deteremine the average utility rates for the searched location. In the United States of America, these are state level averages in US dollars.  In Canada these are national averages in Canadian dollars.

For all searches without a resolved country, state or with a resolved country outside of the United States of America and Canada, the US national average rate will be assumed if the rates are not provided.

The server assumes that the user is entering the cost per unit of utility that is appropriate for the selected unit system. For example if in SI, the user is entering a natural gas rate per cubic meter.

### Natural Gas Rate

> **Name:** `rate_natural_gas`

> **Type:** Float

> **Unit:** cost/100 cubic feet (cost/cubic meter)

> **Default:** varies by location

### Standard Electric Rate

> **Name:** `rate_electric_standard`

> **Type:** Float

> **Unit:** cost/kWh (cost/kWh)

> **Default:** varies by location

### Geothermal Electric Rate

> **Name:** `rate_electric_geo`

> **Type:** Float

> **Unit:** cost/kWh (cost/kWh)

> **Default:** rate_electric_standard

### Propane Rate

> **Name:** `rate_propane`

> **Type:** Float

> **Unit:** cost/US Gallon (cost/liter)

> **Default:** varies by location

### Fuel Oil Rate

> **Name:** `rate_fuel_oil`

> **Type:** Float

> **Unit:** cost/US Gallon (cost/liter)

> **Default:** varies by location