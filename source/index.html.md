---
title: CREE App Docs

language_tabs:
 - Code

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Smartcast LACI Application Documentation

LACI is a web-based admin configuration interface used to setup and manage the SmartCast Link embedded computer.

This documentation will contain the various components used in the Link Administration / Configuration Interface (LACI) software module. 

Language bindings for this documentation include Javascript, AngularJS, HTML and JSON. 

References for Python APIs / Web Services will be included in the future.

Code examples can be viewed in the dark area to the right.

#Dashboard

The dashboard will be the landing page for CREE app LACI.

###HTML / AngularJS:

> Sample HTML template for Dashboard Occupancy & Efficiency tabs

```html
<div class="box clearfix">
    <h2>Occupancy</h2>
    <div class="subbox">
        <h4 class="occupied-title">Most Occupied</h4>
        <div class="sub-header">{{mostOccupied[0].name}} <span class="sml-round">{{mostOccupied[0].group}}</span></div>
        <div class="chart">
            <div id="container-speed"></div>
            <div class="whitebgchart"></div>
        </div>
        <ol class="list-items" ng-repeat="item in mostOccupied" ng-hide="$first">
            <li class="item">
                <span class="count">{{item.count}}.</span>
                <span class="number">{{item.number}}</span>
                <span class="name">{{item.name}}</span>
                <span class="sml-round">{{item.group}}</span>
            </li>
        </ol>
    </div>
    <div class="subbox">
        <h4 class="occupied-title">Least Occupied</h4>
        <div class="sub-header">{{leastOccupied[0].name}} <span class="sml-round">{{leastOccupied[0].group}}</span></div>
        <div class="chart">
            <div id="leastoccupied"></div>
            <div class="whitebgchart"></div>
        </div>
        <ol class="list-items" ng-repeat="item in leastOccupied" ng-hide="$first">
            <li class="item">
                <span class="count">{{item.count}}.</span>
                <span class="number">{{item.number}}</span>
                <span class="name">{{item.name}}</span>
                <span class="sml-round">{{item.group}}</span>
            </li>
        </ol>
    </div>
</div>
<div class="box clearfix efficiency">
    <h2>Efficiency</h2>
    <div class="subbox">
        <h4 class="occupied-title">Most Efficient</h4>
        <div class="sub-header">{{mostEfficient[0].name}} <span class="sml-round">{{mostEfficient[0].group}}</span></div>
        <div class="chart">
            <div id="mefficient"></div>
            <div class="whitebgchart"></div>
        </div>
        <ol class="list-items" ng-repeat="item in mostEfficient" ng-hide="$first">
            <li class="item">
                <span class="count">{{item.count}}.</span>
                <span class="number">{{item.number}}</span>
                <span class="name">{{item.name}}</span>
                <span class="sml-round">{{item.group}}</span>
            </li>
        </ol>
    </div>
    <div class="subbox">
        <h4 class="occupied-title">Least Efficient</h4>
        <div class="sub-header">{{leastEfficient[0].name}} <span class="sml-round">{{leastEfficient[0].group}}</span></div>
        <div class="chart">
            <div id="lefficient"></div>
            <div class="whitebgchart"></div>
        </div>
        <ol class="list-items" ng-repeat="item in leastEfficient" ng-hide="$first">
            <li class="item">
                <span class="count">{{item.count}}.</span>
                <span class="number">{{item.number}}</span>
                <span class="name">{{item.name}}</span>
                <span class="sml-round">{{item.group}}</span>
            </li>

        </ol>
    </div>
</div>
```

The HTML template with bindings in AngularJS used for the Occupancy and Efficiency tabs has been presented in the Code section. 
All the variable data are placed between the {{ double curly braces }}. 

##List of scope variables used in the Dashboard page:

> Sample JSON object array for most occupied spaces

``` javascript
$scope.mostOccupied = [{
    count: "1",
    number: "568",
    name: "Lobby",
    group: "s"
},
{
    count: "2",
    number: "559",
    name: "Hallway 4th Floor",
    group: "s"
}];
```

###$scope.mostOccupied

Parameter | Default | Description
--------- | ------- | -----------
count| integer | Number of fixtures in the most occupied space
number| integer | The unique number for the space
name| string | Name of the space
group| char | Group to which the space belongs

> Sample JSON object array for least occupied spaces

``` javascript
$scope.leastOccupied = [{
    count: "1",
    number: "211",
    name: "OCC_GROUP_93 ",
    group: "m"
},
{
    count: "2",
    number: "251",
    name: "OCC_GROUP_133",
    group: "s"
}];
```

###$scope.leastOccupied

Parameter | Default | Description
--------- | ------- | -----------
count| integer | Number of fixtures in the least occupied space
number| integer | The unique number for the space
name| string | Name of the space
group| char | Group to which the space belongs

> Sample JSON object array for most efficient spaces

``` javascript
$scope.mostEfficient = [{
    count: "1",
    number: "422",
    name: "Office FL2 Sec2",
    group: "l"
},
{
    count: "2",
    number: "420",
    name: "Hallway 1st Floor",
    group: "s"
}];
```

###$scope.mostEfficient

Parameter | Default | Description
--------- | ------- | -----------
count| integer | Number of fixtures in the most efficient space
number| integer | The unique number for the space
name| string | Name of the space
group| char | Group to which the space belongs

> Sample JSON object array for least efficient spaces

``` javascript
$scope.leastEfficient = [{
    count: "1",
    number: "5",
    name: "OCC_GROUP_23",
    group: "s"
},
{
    count: "2",
    number: "17",
    name: "OCC_GROUP_133",
    group: "s"
}];
```

###$scope.leastEfficient

Parameter | Default | Description
--------- | ------- | -----------
count| integer | Number of fixtures in the least efficient space
number| integer | The unique number for the space
name| string | Name of the space
group| char | Group to which the space belongs


#Interactive Screen

##List of scope variables used in the Interactive Screen page:

> Sample JSON Object for floor spaces and their properties

``` javascript
// Pass an object array in JSON data format to $scope.floorSpaces to list all the available floor spaces 
// and their properties ( along with data for OccGroups if any ) so the UI can render the spaces correctly. 
// 'SpaceNumber' - Contains the number to the left in a space.
// 'SpaceFloorDesc' - Contains the description of a specific floor space.
// 'SpaceIndicator' - Contains indicator to indicate 'S' for 'Space'.
// 'OccGroups' - Contains an array of JSON data objects with the above 3 properties.
// Below is a sample template of how the JSON data should look like for UI to display them correctly.

$scope.floorSpaces = [{
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S',
    'Expanded': false,
    'OccGroups': [{
        'SpaceNumber': 430,
        'SpaceFloorDesc': 'OCC_GROUP_84',
        'SpaceIndicator': 'S'
    }, {
        'SpaceNumber': 430,
        'SpaceFloorDesc': 'OCC_GROUP_25',
        'SpaceIndicator': 'S'
    }, {
        'SpaceNumber': 430,
        'SpaceFloorDesc': 'OCC_GROUP_03',
        'SpaceIndicator': 'S'
    }, {
        'SpaceNumber': 430,
        'SpaceFloorDesc': 'OCC_GROUP_93',
        'SpaceIndicator': 'S'
    }]
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}, {
    'SpaceNumber': 430,
    'SpaceFloorDesc': 'Bathroom FL 4',
    'SpaceIndicator': 'S'
}];
```
>Energy Score Value. Below value should be changed as per business logic.

``` javascript
$scope.energyScoreValue = function() {
    
    // Processing / Apply business logic and return integer value
    return 525;
};
```
>Sample Text & Values for all dropdowns used in the interactive page.
>Pass an Object array to $scope.chartTypes to set

``` javascript
$scope.chartTypes = ['Chart', 'Line Chart'];
$scope.networkTypes = ['Network 1', 'Network B', 'Network 7', 'Network A', 'Network 5'];
$scope.sortBy = ['A-Z', 'Z-A'];
```

Parameter | Default | Description
--------- | ------- | -----------
$scope.chartTypes | string array | List of chart types used in the interactive screen
$scope.networkTypes | string array | List of network types used in the interactive screen
$scope.sortBy | string array | List of sort options used in the interactive screen
$scope.floorSpaces | JSON Object array | Array of floor slaces used in the interactive screen
floorSpace.SpaceNumber | integer | Space number of the floor space / occupancy group that will be displayed at the left end within each floor space strip.
floorSpace.SpaceFloorDesc | string | Description of the floor space / occupancy group that will be displayed adjacently to the right of the SpaceNumber within each floor space strip.
floorSpace.SpaceIndicator | char | Space size indicator. Can be any one of the 3 - ( S – small, M – medium, L – large )
floorSpace.Expanded | bool | Used internally to set the values for showing / hiding the occupancy groups in any floor space that contains occupancy groups.
floorSpace.OccGroups | JSON Object array | This will contain a JSON object array identical to the floorSpace array, only excluding the properties: “floorSpace.OccGroups” and “floorSpace.Expanded”. This can be used to configure any occupancy groups within a floor space. Sample JSON object is included in the detailed array below.
$scope.energyScoreValue | integer | Overall Energy Score value. Value will be set based on the business logic of the app.


#LACI Setup Screen

<aside class="warning">

The LACI setup wizard can contain many steps as a process for installation of the LACI app. 
A Sample HTML template is presented to the right of this content.

</aside> 

> Sample code of the template used for a single step of the CREE app (LACI)

```html
<section class="container setup-wizard-container">
    <div class="setup-wizard-area laci">
        <h1 class="setup-wizard-title">LACI Setup </h1>
        <h2 class="setup-wizard-step">Step 1 of 3</h2>
        <div class="setup-wizard-step-contents clearfix">
            <div class="left">
                <h5 class="setup-wizard-form-field">Time Zone</h5>
                <div class="customselect">
                    <select name="speed" id="timezone">
                  <option selected="selected">Eastern</option>
                  <option>Pacific</option>
                  <option>Western</option>
                </select>
                </div>
            </div>
            <div class="right">
                <h5 class="setup-wizard-form-field">Region</h5>
                <div class="customselect">
                    <select name="speed" id="region">
                  <option>Select</option>
                </select>
                </div>
            </div>
        </div>
        <a href="#" class="leftarrow"><i class="fa fa-angle-left" aria-hidden="true"></i></a>
        <a href="#" class="rightarrow"><i class="fa fa-angle-right" aria-hidden="true"></i></a>
    </div>
</section>
```

###List of Classes Used in the sample template for LACI Setup:

1. setup-wizard-area
		
	Use this class to describe the container for the setup wizard.
		
2. setup-wizard-title

	Use this class to describe the container for the title of app setup.

3. setup-wizard-step

	Use this class to configure the step counter in the app setup wizard.

4. setup-wizard-step-contents

	Use this class to describe the container for the contents of a specific step in setup wizard.

5. setup-wizard-form-field

	Use this class to describe the title container for the form field(s) for a 	specific step in setup wizard.