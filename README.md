# comparetout-doc
This page describes the android app "Eco Power Optimisr".

![App icon](./images/ic_launcher.png)
 
To install on android you can : 

[![GetIt](./images/getItOnGooglePlay.png)](https://play.google.com/store/apps/details?id=com.tfcode.comparetout)

## Purpose
The app compares electricity time of use tariffs with data that you provide to get a realistic estimate of expected annual charges.

Time of use tariffs are complex, and the app aims to simplify the process of gathering information and calculating figures useful for comparison.

### Getting started
A quick start guide video is available on [YouTube](https://youtu.be/vUdPhGrInnM)

## Top level concepts
There are three main tabs in the app. Usage, Costs and Comparisons.

![Top tabs](./images/MainTabs.png)
![Add FAB](./images/AddFAB.png)

The comparisons can only be shared.

For usage and cost, you can:
* Load from file
* Download from the internet
* Share with others
* Create a new entry

Once usage and costs have defined (loaded, downloaded, or created)
![DefinedUsage](./images/DefinedUsage.png)

You can:
* Select to be included in the comparison
* View/Edit (by clicking on the text)
* Delete
* Copy to create a new usage/cost based on an existing one


## Usage
### What is a usage
Usage describes how you use and optionally generate electricity.
There are six distinct areas of usage. The only mandatory area is the "Load Profile". All other areas are optional:

* **Load profiles** describe domestic usage of electricity. The are many sources of this data supported in the app.
* **Inverters** convert AC electricity to and from DC. An inverter are required to define solar panels or batteries.
* **Solar panels** provide DC electricity based on physical aspect. There are several sources of solar data supported by the app.
* **Batteries** store DC electricity for later consumption. They have characteristics, and may be charged from the grid based on schedules.
* **Hot water** can be used to store useful energy from solar panels. The app provides a simple model of a how water system and allows for scheduled water heating, and diversion of surplus solar electricity (after normal house load is satisfied).
* **Electric vehicles** can be charged on either a schedule, or using a diversion of surplus solar electricity (after normal house load is satisfied).

![Usage areas](./images/UsageAreas.png)

The button images in the view/edit usage correspond to the usage areas above. A green tick (or absence) indicates if load profile, inverter or panels have been defined.

The green icons on the battery, hot water and EV indicate that settings, schedules and diversions have been configured (or not, shaded icons).

The orange sun on the panels lets you know that PV data is associated with the solar panels. Without the sun, the simulation will not run!

Once the mandatory areas are configured, the app will automatically simulate usage and generate costs (at least one cost must be defined) for a single year. When simulation is complete some key overview indicators are provided.

![KeyIndicators](./images/KeyIndicators.png)
* The best cost found
* The supplier and plan that provided the cost
* The amount of generated electricity (if applicable) used and exported
* The amount of used electricity that was purchased and generated

The DAILY DETAILS, MONTHLY ROLLUP and YEAR SUMMARY tabs will also be populated when the simulation is complete. You can navigate the simulation output to get an insight into why the costs are the way they are.
![DailyDetails](./images/DailyDetails.png)
### Usage area details
A usage must be saved with a unique name before adding any usage area. Newly created usage will be in edit mode already. 

#### Load Profile
Load profiles are the only mandatory usage area. 

A load profile consists of some basic usage data and three distributions. The app allows you to use standard load profiles (STANDARD LOAD PROFILE), generate a load profile from an ESBN HDF file (ESBN HDF FILE), or create manually based on your understanding of your usage (CUSTOM).

![LoadProfileOverview](./images/LoadProfileOverview.png)

Distributions show how electricity usage is spread across hours, days, months. This accounts for habit and seasonal variations. Each distribution totals 100% of andual usage.

![HourlyDistribution](./images/HourlyDistribution.png)

When you edit a load profile, you can import from a file, copy from or link to a load profile defined in another usage.

![ImportLinkCopy](./images/LoadProfileLinkCopyImport.png)

Linking or copying will show a list of usages that can be used as source.

![LinkDialog](./images/LinkDialog.png)

When usage areas are linked, a link icon appears in the bottom left of the screen. Clicking on this icon will show a list of the usages that are linked.

![LinkIcon](./images/LinkIcon.png)

In edit mode, it is also possible to select a standard load profile. Standard load profiles are published annually by ESBN. These are from Nov 2022.

![StandardLoadProfile](./images/LoadProfileSource.png)

More load profile sources will be added in later versions of the app. For now a simple editor is provided if the standard load profiles do not satisfy.

![EditDistribution](./images/EditDistribution.png)

#### Inverters
Inverters are key components in how solar/battery systems are connected to you house. They are not perfect, energy is lost (in the form of heat) whenever a DC <-> AC conversion happens.

This area captures the key characteristics of an inverter, capacity and losses for the various conversions, the number of ports (for solar panels) and the minimum excess required before battery charging will happen.

All of this information should be abailable from the manufacturer specification. A good round trip estimation for loss is 20%.

Inverter names need to be unique within a usage. The inverter name is used to connect panels and batteries to the house.

![InverterOverview](./images/InverterOveriew.png)

When editing, you can import, copy, link delete and add an inverter.

![InverterOperations](./images/InverterOperations.png)
![Add](./images/AddFAB.png)

Multiple hybrid string inverters are quite tricky in the real world. Please get professional advice before having more than one inverter attached to you home.

#### Solar Panels
Solar panels are connected to inveter ports (MPPT -- Maximum Power Point Tracking). To distinguish different strings a name is needed. The number of panels in a string and the maximim power output is needed. When a panel (string) is fully configured the monthly generation is shown at the bottom of the screen. A usage with panels, but no generation data is not eligible for comparison.

![PanelOverview](./images/PanelOverview.png)

Editing panels allows for import, copy, link, add, delete, and fetching data

![PanelOperations](./images/PanelOperations.png)
![Add](./images/AddFAB.png)

If the monthly generation is missing from the bottom of the screen, or you would like to refresh it, you can fetch/update data. For now only a single data source is supported. Later version of the app will add more.

![PVGIS](./images/PVGISGrabber.png)

The information on this screen is stored on you device. Location data can be refreshed using the current location on your device (if available/permitted). The data is used to query the PVGIS database. Data downloaded from PVGIS is stored as-is in your downloads folder. Relevant data is extracted from this file and added to the apps internal DB.

Deleting the panel will remove all of this data from the device.

#### Batteries

Batteries may be configured and scheduled for charging. Clicking on the battery image will open a menu.

![BatteryMenu](./images/BatteryMenu.png)

##### Battery configuration

Battery configuration associates a battery with one of the inverters defined above. Some vital statistics are also needed to simulate correctly.
* How big is the battery
* At what percentage should discharge be stopped
* How much can the battery provide in 5 minutes
* How much can the battery charge in 5 minutes
* How much energy is lost by storing in the battery

![BatteryOverview](./images/BatteryOverview.png)

Batteries (really battery management systems) try to protect themselves. When they are completely depeleted or nearly full, the charge rate drops. The app uses a simple model that reduces the maximum charge rate to a percentage based on the state of charge.

Editing the battery allows for import, copy, link add and delete.

![BatteryOperations](./images/BatteryOperations.png)
![Add](./images/AddFAB.png)


##### Scheduling battery charging from grid (Purchase shifting)
Purchase shifting (scheduled charging of the battery from the grid) can make a huge difference to the annual cost, and repayment time -- if there is a big difference between hourly rates.

![BatterySchedule](./images/BatteryCharging.png)

Battery charging schedules must be associated with an inverter. You may have several batteries associated with an inverter, they will all be charged/discharged together.

Charging schedules are applied on a day-of-week and month-of-year basis. New schedules can be created using the + button (when editing). On any given day multiple charging sessions can be defined. Each session includes a maximum charge point. All batteries associated with an inverter will not service house load during a charging session, even if the maximum has been achieved.

#### Hot water
Hot water systems will be described later.
#### Electric Vehicle
Electriv vehicles will be described later.

## Cost
As mentioned above, costs can be added by loading from a file, downloading or creating. Suppliers typically refer to these as price plans -- both terms are used here.

When you first create a cost (price plan), it is not valid. This is indicated by the red banner at the top.

![NewPricePlan](./images/PricePlanNew.png)

Clicking the (i) info icon will provide a short explanantion. It is not possible to save an invalid price plan.

![InvalidPricePlan](./images/PricePlanInvalid.png)

The main tab of a price plan captures basic information about the plan:
* Supplier
* Plan name
* Export price
* Fixed charges
* Welcome discounts
* Last update (plans change requently, always check details before making decisions)
* Reference (where the information came from)

Price plans do not cover all terms and conditions. Please check the detail and correctness  of a plan before signing up!

Editing a price plan also allows the addition and removal of day rates.

![PricePlanOperations](./images/PricePlanEdit.png)

Adding a day rate makes the price plan valid. It can be saved and shared. A new tab is also added for each day rate.

![PricePlanOK](./images/PricePlanOK.png)

Day rates capture the cost of electricity by hour, day of week and date. Every date in the year, day of the week and hour of the day needs to have a cost. Additional day rates are needed for price plans that vary by weekday or calendar date. In this example, a second day rate is needed to capture the price of electricity on Saturday.

![DayRate](./images/DayRate.png)

Rows can be added and deleted. The first row will always be from 0, and the last to 24.

## Compare

All selected costs are applied to all selected usages. The combined selection is visible in the comparison tab.

![ComparisonPortrait](./images/ComparePortrait.png)

With long names, this can be a bit cramped. You can show less columns, or rotate the device to landscape.

![ComparisonLandscape](./images/CompareLandscape.png)

For longer lists, the table may be sorted.

Clicking on a row provides a pie chart that shows the percentage of purchased electricity at each price point in the price plan.

![ComparePie](./images/ComparePie.png)

## Warning
This software is in development. There are still far too many crashes. 

It should be used only to provide an estimate indication of comparative cost.
The software comes with absolutely no guarantees. 