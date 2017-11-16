---
title: Genivity Calculator API Reference

language_tabs:
  - curl
toc_footers:
  - <a href='https://www.genivity.com/halo'>Go to Genivity Site</a>

includes:
  - errors

---

# Introduction

Welcome to the Genivity Calculator API! You can use our API to access Genivity Calculator API endpoints, which can get information on genetic age, expected life span and care costs.

Health and wealth are closely knit together in financial planning. Poor health habits almost always wind up costing people money and health care will be many people’s largest expense in retirement (Rozen, 2014). On the other hand, those who are healthy are more likely to exceed average life expectancy requiring a large nest egg to ensure they don’t outlive their assets.

Even the most well-intended plans can crumble in a second when faced with a sudden death, disability or long-term-care need.

That is why we introduce `HALO (HEALTH ANALYSIS & LONGEVITY OPTIMIZER)` that helps you to understand:

* How many active and healthy years you can look forward to
* How many years where you’ll potentially need additional help with daily care (assisted living facilities / in-home care) and what your estimated costs would be for that care
* What to expect for out-of-pocket care costs throughout your lifespan and how those costs change at different life stages.

# Genivity Calculation

## Sample Request and Response 

> API Endpoint:

```
POST https://tapgenes.com/ehr/v1/genevitycalculation
```
> Sample Request

```bash
curl -X POST --header 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36' --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "ethnicity":{
 	"European ancestry":50,
 	"African ancestry":30,
 	"Asian ancestry":20,
 	"Hispanic ancestry":0,
 	"Other ancestry":0
  },
  "firstName":"FIRST_NAME",
  "lastName":"LAST_NAME",
  "email":"EMAIL",
  "gender":"male",
  "age":"70",
  "isExercise":false,
  "isSmoker":true,
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "weight":185,
  "height":65,
  "retirementAge":"65",
  "retirementPlace":"California",
  "longLivedMemberCount":"3",
  "doctorVisitFrequency":"average",
  "fromSource":"FROM_SOURCE_URL"
}' 'https://tapgenes.com/ehr/v1/phr/genevitycalculation'
```
> Make sure you replace the following:

```
FROM_SOURCE_URL - The URL of the site from which the HALO is accessed from. (For example: https://www.sample.com/path/)
EMAIL - A valid e-mail
FIRST_NAME - First Name of the user who takes the assessment
LAST_NAME - Last Name of the user who takes the assessment
```
>Sample Response:

```json
{
  "age": 70,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "firstName": "firstname",
  "lastName": "lastname",
  "email": "person@sample.com",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
    "lifeStyleImpactRetirementAge": {
      "exerciserNonSmokerIdealBmi": 9,
      "idealBmi": -4,
      "exerciser": -4,
      "nonSmokerIdealBmi": 4,
      "exerciserNonSmoker": 7,
      "exerciserIdealBmi": -3,
      "nonSmoker": 3
    },
    "expectedHealthyYears": 0,
    "expectedYearsInHomeCare": 4,
    "activeRetirementAge": 0,
    "exerciserNonSmokerMaxCareCost": 665372.2286233829,
    "nonSmokerMaxCareCost": 764873.6930477947,
    "exerciserNonSmokerIdealBmiMaxCareCost": 457324.6166583799,
    "expectedYearsLost": 13,
    "idealBmiRange": [
      "BMI_19",
      "BMI_20",
      "BMI_21",
      "BMI_22",
      "BMI_23",
      "BMI_24",
      "BMI_25",
      "BMI_26",
      "BMI_27",
      "BMI_28",
      "BMI_29",
      "BMI_30",
      "BMI_31",
      "BMI_32",
      "BMI_33",
      "BMI_34",
      "BMI_35"
    ],
    "expectedCareCost": 42884,
    "homeCareTotalCost": 204113.307495123,
    "nursingHomeTotalCost": 118880.2104,
    "lifeStyleImpactCareCost": {
      "exerciserNonSmokerIdealBmi": 79318,
      "idealBmi": 21340,
      "exerciser": 21340,
      "nonSmokerIdealBmi": 60097,
      "exerciserNonSmoker": 79318,
      "exerciserIdealBmi": 21340,
      "nonSmoker": 60097
    },
    "exerciserMaxCareCost": 465624.1647687048,
    "exerciserIdealBmiMaxCareCost": 465624.1647687048,
    "probabilityOfLivingNinetyFive": 9.3,
    "probabilityOfLivingNinety": 29.3,
    "activeYearsWithLongLive": 0,
    "careCostBreakDown": {
      "belSevenFourAnnual": "$5,335.00",
      "belSixFourTotal": "$0.00",
      "belEighteenAnnual": "$1,496.00",
      "belEightFourAnnual": "$6,407.00",
      "aboveEightFiveTotal": "$0.00",
      "belEighteenTotal": "$0.00",
      "belSevenFourTotal": "$22,319.65",
      "retirementOutOfPacketCareCost": "$22,319.65",
      "belSixNineAnnual": "$4,137.00",
      "belSixNineTotal": "$0.00",
      "belSevenNineAnnual": "$5,403.00",
      "belSevenNineTotal": "$0.00",
      "totalOutOfPacketCareCost": "$22,319.65",
      "belEightFourTotal": "$0.00",
      "aboveEightFiveAnnual": "$9,469.00",
      "belSixFourAnnual": "$1,950.00"
    },
    "expectedTotalHealthyYears": -3,
    "lifeStyleDisabilityYears": {
      "exerciserNonSmokerIdealBmi": 4.022322493000001,
      "idealBmi": 3,
      "exerciser": 3.2300000190734863,
      "nonSmokerIdealBmi": 6.022322493000001,
      "exerciserNonSmoker": 6.022322493000001,
      "exerciserIdealBmi": 3.2300000190734863,
      "nonSmoker": 7.022322493000001
    },
    "expectedYearsInAssessedLiving": 2,
    "assessedLivingTotalCost": 97440,
    "calculatedBMI": 31,
    "lifeStyleHealthyYears": {
      "exerciserNonSmokerIdealBmi": 0.20767704923632735,
      "idealBmi": 0,
      "exerciser": 0.20767752607348555,
      "nonSmokerIdealBmi": 0.20767704923632735,
      "exerciserNonSmoker": 0.20767704923632735,
      "exerciserIdealBmi": 0.20767752607348555,
      "nonSmoker": 0.20767704923632735
    },
    "yearlyCareCostByState": {
      "homemakerYearlyHealthAideCost": 54912,
      "homemakerServicesTotalCost": 106818.6,
      "homemakerServicesYearlyCost": 52620,
      "assistedLivingYearlyPrivateRoomCost": 48000,
      "maxCareCost": 227473.68,
      "nursingHomeSemiYearlyPrivateRoomCost": 91248,
      "adultDayHealthTotalCareCost": 40632.479999999996,
      "nursingHomeTotalPrivateRoomCost": 227473.68,
      "homemakerTotalHealthAideCost": 111471.36,
      "nursingHomeSemiTotalPrivateRoomCost": 185233.44,
      "adultDayHealthYearlyCareCost": 20016,
      "minCareCost": 40632.479999999996,
      "assistedLivingTotalPrivateRoomCost": 97440,
      "nursingHomeYearlyPrivateRoomCost": 112056
    },
    "expectedDisabilityYears": 3,
    "diseaseRecommentation": {
      "Stroke": [
        "Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
        "Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
        "Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
      ],
      "Alzheimers Disease": [
        "Engage in social and intellectually stimulating activities",
        "Exercise regularly and eat a healthy diet rich in fruits and vegetables",
        "Maintain a healthy weight and get treatment for depression (if applicable)"
      ],
      "Heart Disease": [
        "Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
        "Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
        "Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
      ]
    },
    "probabilityOfLivingHundred": 1.7,
    "idealBmiMaxCareCost": 227473.68,
    "nonSmokerIdealBmiMaxCareCost": 665372.2286233829,
    "lifeStyleYearsLost": {
      "exerciserNonSmokerIdealBmi": 0,
      "idealBmi": 13,
      "exerciser": 10,
      "nonSmokerIdealBmi": 3,
      "exerciserNonSmoker": 0,
      "exerciserIdealBmi": 10,
      "nonSmoker": 3
    },
    "expectedYearsInNursingHome": 1,
    "totalCareCost": 420433.517895123
  },
  "cancerTypes": [],
  "longLivedMemberCount": 3,
  "doctorVisitFrequency": "average",
  "retirementAge": 65,
  "states": [],
  "retirementPlace": "California",
  "ethnicity": {
    "European ancestry": 50,
    "African ancestry": 30,
    "Asian ancestry": 20,
    "Hispanic ancestry": 0,
    "Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 62.0.3202.94 Linux",
  "genivityAdviser": {
    "id": 123,
    "name": "adviser",
    "email": "adviser@organization.com",
    "siteUrl": "https://sample.com/path/",
    "isActive": 1,
    "address": "5, 2nd Street, Somewhere.",
    "phoneNumber": "4578123544",
    "firmName": "Genivity Inc.Ltd."
  }
}
```

Genivity Calculator uses the From Source URL to allow access to the API. Only the requests from the whitelisted from source URL will be served.

## Body Params

### Ethinicity
	
> If a person’s ancestry is European, the ethnicity value should be :

```json
{
    "ethnicity": {
        "European ancestry": 100,
        "African ancestry": 0,
        "Asian ancestry": 0,
        "Hispanic ancestry": 0,
        "Other ancestry": 0
    }
}
```
> If the person’s ancestry is half Asian and half African, the ethnicity value should be :

```json
{
    "ethnicity": {
        "European ancestry": 0,
        "African ancestry": 50,
        "Asian ancestry": 50,
        "Hispanic ancestry": 0,
        "Other ancestry": 0
    }
}
```
> If the person’s ancestry does not come under the four categories: European, African, Asian and Hispanic, the ethnicity value should be :

```json
{
    "ethnicity": {
        "European ancestry": 0,
        "African ancestry": 0,
        "Asian ancestry": 0,
        "Hispanic ancestry": 0,
        "Other ancestry": 100
    }
}
```
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
ethinicity | false | Map&lt;String, Integer&gt; | The percentage value of a person’s ancestry. The sum of all the values should be 100.

### First Name
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
firstName | false | String | The first name of the user who takes the assessment.

### Last Name
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
lastName | false | String | The last name of the user who takes the assessment.

### Email
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
email | false | String | The email address of the user who takes the assessment. An email will be sent to this email address once the assessment is finished and the result is generated.

### Gender
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
gender | true | String | The gender of the user (male or female).

### Age
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
age | true | Integer | The age of the user at the time of taking the assessment.

### Retirement Age
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
retirementAge | false | Integer | The age at which the user wishes to retire or already retired.

### Retirement State
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
retirementPlace | false | String | The place at which the user wishes to stay after their retirement.

### Long Lived Member Count
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
longLivedMemberCount | false | Integer | The number of persons in the user’s family who have lived to certain age. This age range will be the sum of the user’s current age, user’s expected total healthy years and user’s expected disable years.

### Doctor Visit Frequency

> If the visit count comes under 0-2 times, the value should be:

```json
{
    "doctorVisitFrequency":"belowAverage"
}
```

> If the visit count comes under 3-5 times, the value should be:

```json
{
    "doctorVisitFrequency":"average"
}
```

> If the visit count is more than 5 times, the value should be:

```json
{
    "doctorVisitFrequency":"aboveAverage"
}
```

Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
doctorVisitFrequency | false | String | The number of times the user visits a doctor in a year.

### Exercise
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
isExercise | false | Boolean | Does the user a regular exerciser? If Yes, the value is true. If no, the value is false.

### Smoker
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
isSmoker | false | Boolean | Does the user smoker? If Yes, the value is true. If no, the value is false.

### Stroke
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
havingStroke | true | Boolean | Does any of the user’s immediate family members (parents, siblings, children,or user itself) been diagnosed with stroke? If Yes, the value is true. If no, the value is false.

### Diabetes
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
havingDiabetes | true | Boolean | Does any of the user’s immediate family members (parents, siblings, children,or user itself) been diagnosed with Type 2 Diabetes? If Yes, the value is true. If no, the value is false.

### Heart Disease
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
havingHeartDisease | true | Boolean | Does any of the user’s immediate family members (parents, siblings, children,or user itself) been diagnosed with Heart Disease? If Yes, the value is true. If no, the value is false.

### Alzheimer's Disease
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
havingAlzheimer | true | Boolean | Does any of the user’s immediate family members (parents, siblings, children,or user itself) been diagnosed with Alzheimer’s? If Yes, the value is true. If no, the value is false.

### Cancer Types
> Sample Input:

```json
{
    "cancerTypes": [
        "Kidney Cancer",
        "Lung Cancer",
        "Ovarian Cancer",
        "Prostate Cancer"
    ]
}
```
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
cancerTypes | true | Array[String] | Array of Cancer types which any of the user’s immediate family members (parents, siblings, children,or user itself) have been diagnosed with.

The options for the cancer types will be:
* Bladder Cancer
* Breast Cancer
* Colorectal Cancer
* Kidney Cancer
* Lung Cancer
* Ovarian Cancer
* Pancreatic Cancer
* Prostate Cancer
* Melanoma Skin Cancer
* Other

If no one is diagnosed with Cancer, the cancerTypes array should be empty.

### Weight
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
weight | false | Float | The weight of the user in Pounds(lbs).

### Height
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
height | false | Float | The height of the user in Inches.

### From Source URL
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
fromSource | true | String | The URL of the site from which the HALO is accessed from.

### Country
Parameter | Default | Type | Description
--------- | ------- | ---- | -------------
country | false | String | The country from which the user is taking the assessment. This is used to retrieve the states which is used as options for retirement place. This value is set to ‘United States’ by default.

## Output Description
The result JSON is explained below.

Result | Type | Description
-------| ---- | -------------
states | List<String> | The name of the states present in the given country. These values can be used as options while getting the retirement place from the user.
results | Map&lt;String, Object&gt; | The results (mentioned in the following table) of the genivity calculation are put in this map.

### Genivity Results
Key | Type | Description
--------- | ---- | -------------
probabilityOfLivingNinety | Float | The probability of the person living to ninety years.
probabilityOfLivingNinetyFive | Float | The probability of the person living to ninety five years.
probabilityOfLivingHundred | Float | The probability of the person living to hundred years.
diseaseRecommentation | Map&lt;String, List&lt;String&gt;&gt; | The preventive measures a person can take for the given disease. This map contains the disease name as the key and the list of preventive steps as the value.
calculatedBMI | long | The BMI value calculated from the given height and weight.
idealBmiRange |  List&lt;String&gt; | The ideal BMI range for the given age and gender is calculated and given as List of String. The String contains the BMI value with the prefix of “BMI_”. The list value ranges from the minimum BMI value to the maximum BMI value a person of the given age and gender can have. If the calculated BMI obtained in the result is within the BMI value range in this list, then the calculated BMI is an ideal BMI.
expectedYearsLost | double | The years lost from a person’s life span due to the person’s height, weight, smoking and exercise habits.
expectedDisabilityYears | double | The time period a person will be disabled in the life span, due to the diseases the person is diagnosed with.
activeYearsWithLongLive | double | The expected healthy years of a person without the long lived member count adjustment.
expectedTotalHealthyYears | double | The expected years a person with the long lived member count adjustment. This value is counted for calculating the age upto which the most family members lived.
lifeStyleDisabilityYears | Map&lt;String, Object&gt; | The time period a person will be disabled in the life span, for all the combinations of the person’s habits like smoking, exercising and ideal BMI. For instance, the disability years for a person, whose BMI fall under the ideal BMI range and also a regular exerciser, can be found in the value of the key “exerciserIdealBmi”.
lifeStyleYearsLost | Map&lt;String, Object&gt; | The years lost from a person’s life span, for all the combinations of the person’s habits like smoking, exercising and ideal BMI. For instance, the years lost for a person, whose BMI does not fall under the ideal BMI range, who is a non-smoker and also a regular exerciser, can be found in the value of the key “exerciserNonSmoker”.
expectedHealthyYears | double | The time period a person will be healthy and active in the life span, calculated for the given diseases and lifestyle.
activeRetirementAge | double | The time period a person will be healthy and active in the life span, calculated for the given diseases and lifestyle.
lifeStyleHealthyYears | Map&lt;String, Object&gt; | The time period a person will be healthy and working in the life span, for all the combinations of the person’s habits like smoking, exercising and ideal BMI. For instance, the healthy working years for a person, whose BMI fall under the ideal BMI range, who is a smoker and does not exercise regularly, can be found in the value of the key “idealBmi”.
lifeStyleImpactRetirementAge | Map&lt;String, Object&gt; | The time period a person will be healthy during the retirement phase in the life span, for all the combinations of the person’s habits like smoking, exercising and ideal BMI. For instance, the healthy working years for a person, whose BMI fall under the ideal BMI range, who is a smoker and does not exercise regularly, can be found in the value of the key “idealBmi”.
yearlyCareCostByState | Map&lt;String, Double&gt; | The total expenditure of the person for all five types of care in the state which the person chose to stay, during his disability years. For instance, the person chose California for staying after retirement and is having 4 years of disability years, the care cost amount will be calculated for 4 years for all types of care in California. The care cost vary among states and the type of care. This result contain both total and yearly care cost for all type of care. This also contains the maximum and minimum care cost amount among all types. The care cost is in US Dollars ($).
nonSmokerMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for his disability years if he is a non-smoker.
exerciserMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for the disability years if he is an exerciser.
idealBmiMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for the disability years if he has an ideal BMI.
exerciserNonSmokerMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for the disability years if he is an exerciser and non-smoker.
exerciserNonSmokerIdealBmiMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for the disability years if he is an exerciser, non-smoker and has an ideal BMI.
nonSmokerIdealBmiMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for the disability years if he is a non-smoker and has an ideal BMI.
exerciserIdealBmiMaxCareCost | Double | The maximum expenditure of the person among all five types of care costs in the state which the person chose to stay, for the disability years if he is an exerciser and has an ideal BMI.
expectedYearsInHomeCare | int | The number of years a person is expected to be in Home Care.
homeCareTotalCost | double | The care cost expenditure of a person for his expected years in Home Care.
expectedYearsInAssessedLiving | int | The number of years a person is expected to be under assistance.
assessedLivingTotalCost | double | The care cost expenditure of a person for his expected years under assistance.
expectedYearsInNursingHome | int | The number of years a person is expected to be in Nursing Home Care.
nursingHomeTotalCost | double | The care cost expenditure of a person for his expected years Nursing Home Care.
totalCareCost | double | The total care cost expenditure of a person for his expected years in Home Care, assisted living and Nursing Home Care.
careCostBreakDown | Map&lt;String, String&gt; | This care costs include the financial costs associated with care and the treatment of the disease itself (e.g., doctor visits, surgeries, prescriptions, co-pays, premium payments, etc.). This map contains both the total and annual  Out of Pocket Care Cost for the pre-defined age category, Out of Pocket Care Cost for retirement years and Out of Pocket Care Cost for total lifetime.

## Sample Input JSON and Output JSON

We present you with the sample input JSON and their corresponding output JSON for reference.

### States

> Input JSON:

```json
{
  "fromSource":"https://www.sample.com/path/",
  "country":"United States"
}
```
> Output JSON:

```json
{
  "fromSource": "https://www.sample.com/path/",
  "results": {},
  "country": "United States",
  "states": [
    "Alabama",
    "Alaska",
    "Arizona",
    "Arkansas",
    "California",
    "Colorado",
    "Connecticut",
    "Delaware",
    "District of Columbia",
    "Florida",
    "Georgia",
    "Hawaii",
    "Idaho",
    "Illinois",
    "Indiana",
    "Iowa",
    "Kansas",
    "Kentucky",
    "Louisiana",
    "Maine",
    "Maryland",
    "Massachusetts",
    "Michigan",
    "Minnesota",
    "Mississippi",
    "Missouri",
    "Montana",
    "Nebraska",
    "Nevada",
    "New Hampshire",
    "New Jersey",
    "New Mexico",
    "New York",
    "North Carolina",
    "North Dakota",
    "Ohio",
    "Oklahoma",
    "Oregon",
    "Pennsylvania",
    "Rhode Island",
    "South Carolina",
    "South Dakota",
    "Tennessee",
    "Texas",
    "Utah",
    "Vermont",
    "Virginia",
    "Washington",
    "West Virginia",
    "Wisconsin",
    "Wyoming"
  ],
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To retrieve the list of states.

### Disease Recommendation and Probability of Living to 90, 95 and 100 years

> Input JSON:

```json
{
  "gender":"male",
  "age":"70",
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "fromSource":"https://www.sample.com/path/"
}
```
> Output JSON:

```json
{
  "age": 70,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
	"probabilityOfLivingNinetyFive": 0,
	"probabilityOfLivingNinety": 0,
	"diseaseRecommentation": {
  	"Stroke": [
    	"Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
    	"Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
    	"Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
  	],
  	"Alzheimers Disease": [
    	"Engage in social and intellectually stimulating activities",
    	"Exercise regularly and eat a healthy diet rich in fruits and vegetables",
    	"Maintain a healthy weight and get treatment for depression (if applicable)"
  	],
  	"Type 2 Diabetes": [
    	"Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
    	"Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
    	"Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
  	],
  	"Heart Disease": [
    	"Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
    	"Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
    	"Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
  	]
	},
	"probabilityOfLivingHundred": 1.7
  },
  "cancerTypes": [],
  "states": [],
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To get the recommendation details for the given diseases and the person's probability of living to ninety, ninety five and hundred years.

### Calculated BMI and Expected Years Lost

> Input JSON:

```json
{
  "gender":"male",
  "age":"70",
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "isExercise":false,
  "isSmoker":true,
  "weight":185,
  "height":65,
  "ethnicity":{
 	"European ancestry":50,
 	"African ancestry":25,
 	"Asian ancestry":25,
 	"Hispanic ancestry":0,
 	"Other ancestry":0
  },
  "fromSource":"https://www.sample.com/path/"
}
```
> Output JSON:

```json
{
  "age": 70,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
	"probabilityOfLivingNinetyFive": 0,
	"expectedYearsLost": 13,
	"probabilityOfLivingNinety": 0,
	"diseaseRecommentation": {
  	"Stroke": [
    	"Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
    	"Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
    	"Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
  	],
  	"Alzheimers Disease": [
    	"Engage in social and intellectually stimulating activities",
    	"Exercise regularly and eat a healthy diet rich in fruits and vegetables",
    	"Maintain a healthy weight and get treatment for depression (if applicable)"
  	],
  	"Type 2 Diabetes": [
    	"Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
    	"Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
    	"Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
  	],
  	"Heart Disease": [
    	"Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
    	"Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
    	"Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
  	]
	},
	"probabilityOfLivingHundred": 1.7,
	"calculatedBMI": 31
  },
  "cancerTypes": [],
  "states": [],
  "ethnicity": {
	"European ancestry": 50,
	"African ancestry": 25,
	"Asian ancestry": 25,
	"Hispanic ancestry": 0,
	"Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To get the BMI of the person and the expected number of years lost in their lifetime.

### Expected Disability Years, Active Years With Long Live, Expected Total Healthy Years, Ideal Bmi Range, Life Style Disability Years and Life Style Years Lost

> Input JSON:

```json
{
  "gender":"male",
  "age":"30",
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "isExercise":false,
  "isSmoker":true,
  "weight":185,
  "height":65,
  "ethnicity":{
 	"European ancestry":50,
 	"African ancestry":25,
 	"Asian ancestry":25,
 	"Hispanic ancestry":0,
 	"Other ancestry":0
  },
  "longLivedMemberCount":"3",
  "fromSource":"https://www.sample.com/path/"
}
```
> Output JSON:

```json
{
  "age": 30,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
    "probabilityOfLivingNinetyFive": 0,
    "expectedYearsLost": 15,
    "expectedDisabilityYears": 7.022322493000001,
    "probabilityOfLivingNinety": 0,
    "idealBmiRange": [
      "BMI_22",
      "BMI_23",
      "BMI_24",
      "BMI_25",
      "BMI_26"
    ],
    "diseaseRecommentation": {
      "Stroke": [
        "Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
        "Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
        "Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
      ],
      "Alzheimers Disease": [
        "Engage in social and intellectually stimulating activities",
        "Exercise regularly and eat a healthy diet rich in fruits and vegetables",
        "Maintain a healthy weight and get treatment for depression (if applicable)"
      ],
      "Type 2 Diabetes": [
        "Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
        "Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
        "Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
      ],
      "Heart Disease": [
        "Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
        "Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
        "Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
      ]
    },
    "activeYearsWithLongLive": 27.46767537076953,
    "expectedTotalHealthyYears": 24.46767537076953,
    "lifeStyleDisabilityYears": {
      "exerciserNonSmokerIdealBmi": 4.022322493000001,
      "idealBmi": 7.022322493000001,
      "exerciser": 7.022322493000001,
      "nonSmokerIdealBmi": 6.022322493000001,
      "exerciserNonSmoker": 6.022322493000001,
      "exerciserIdealBmi": 6.022322493000001,
      "nonSmoker": 7.022322493000001
    },
    "probabilityOfLivingHundred": 2.8,
    "lifeStyleYearsLost": {
      "exerciserNonSmokerIdealBmi": 0,
      "idealBmi": 13,
      "exerciser": 12,
      "nonSmokerIdealBmi": 3,
      "exerciserNonSmoker": 2,
      "exerciserIdealBmi": 10,
      "nonSmoker": 5
    },
    "calculatedBMI": 31
  },
  "cancerTypes": [],
  "longLivedMemberCount": 3,
  "states": [],
  "ethnicity": {
    "European ancestry": 50,
    "African ancestry": 25,
    "Asian ancestry": 25,
    "Hispanic ancestry": 0,
    "Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To get the expected number of years the person will be disabled, the expected number of years the person will be active, the expected total number of years the person will be healthy, the number of disability years and years lost for all combinations of their lifestyle.

### Expected Healthy Years, Active Retirement Age, Life Style Healthy Years, Lifestyle Impact Retirement Age

> Input JSON:

```json
{
  "gender":"male",
  "age":"70",
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "isExercise":false,
  "isSmoker":true,
  "weight":185,
  "height":65,
  "ethnicity":{
 	"European ancestry":50,
 	"African ancestry":25,
 	"Asian ancestry":25,
 	"Hispanic ancestry":0,
 	"Other ancestry":0
  },
  "longLivedMemberCount":"3",
  "retirementAge":"65",
  "fromSource":"https://www.sample.com/path/"
}
```
> Output JSON:

```json
{
  "age": 30,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
    "lifeStyleImpactRetirementAge": {
      "exerciserNonSmokerIdealBmi": 10,
      "idealBmi": 0,
      "exerciser": 0,
      "nonSmokerIdealBmi": 5,
      "exerciserNonSmoker": 6,
      "exerciserIdealBmi": 0,
      "nonSmoker": 2
    },
    "probabilityOfLivingNinetyFive": 0,
    "probabilityOfLivingNinety": 0,
    "expectedHealthyYears": 27.46767537076953,
    "activeYearsWithLongLive": 27.46767537076953,
    "expectedTotalHealthyYears": 24.46767537076953,
    "lifeStyleDisabilityYears": {
      "exerciserNonSmokerIdealBmi": 4.022322493000001,
      "idealBmi": 7.022322493000001,
      "exerciser": 7.022322493000001,
      "nonSmokerIdealBmi": 6.022322493000001,
      "exerciserNonSmoker": 6.022322493000001,
      "exerciserIdealBmi": 6.022322493000001,
      "nonSmoker": 7.022322493000001
    },
    "activeRetirementAge": 0,
    "calculatedBMI": 31,
    "lifeStyleHealthyYears": {
      "exerciserNonSmokerIdealBmi": 35.46767537076953,
      "idealBmi": 29.46767537076953,
      "exerciser": 30.46767537076953,
      "nonSmokerIdealBmi": 35.46767537076953,
      "exerciserNonSmoker": 35.46767537076953,
      "exerciserIdealBmi": 33.46767537076953,
      "nonSmoker": 35.46767537076953
    },
    "expectedYearsLost": 15,
    "expectedDisabilityYears": 7.022322493000001,
    "idealBmiRange": [
      "BMI_22",
      "BMI_23",
      "BMI_24",
      "BMI_25",
      "BMI_26"
    ],
    "diseaseRecommentation": {
      "Stroke": [
        "Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
        "Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
        "Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
      ],
      "Alzheimers Disease": [
        "Engage in social and intellectually stimulating activities",
        "Exercise regularly and eat a healthy diet rich in fruits and vegetables",
        "Maintain a healthy weight and get treatment for depression (if applicable)"
      ],
      "Type 2 Diabetes": [
        "Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
        "Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
        "Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
      ],
      "Heart Disease": [
        "Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
        "Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
        "Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
      ]
    },
    "probabilityOfLivingHundred": 2.8,
    "lifeStyleYearsLost": {
      "exerciserNonSmokerIdealBmi": 0,
      "idealBmi": 13,
      "exerciser": 12,
      "nonSmokerIdealBmi": 3,
      "exerciserNonSmoker": 2,
      "exerciserIdealBmi": 10,
      "nonSmoker": 5
    }
  },
  "cancerTypes": [],
  "longLivedMemberCount": 3,
  "retirementAge": 65,
  "states": [],
  "ethnicity": {
    "European ancestry": 50,
    "African ancestry": 25,
    "Asian ancestry": 25,
    "Hispanic ancestry": 0,
    "Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To get the expected number of years the person will be healthy, the time period the person will be active during their retirement phase, the number of active retirement years and expected healthy years for all combinations of their lifestyle.

### Yearly Care Cost for Disability Years and Support Care Cost

> Input JSON:

```json
{
  "gender":"male",
  "age":"70",
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "isExercise":false,
  "isSmoker":true,
  "weight":185,
  "height":65,
  "ethnicity":{
 	"European ancestry":50,
 	"African ancestry":25,
 	"Asian ancestry":25,
 	"Hispanic ancestry":0,
 	"Other ancestry":0
  },
  "longLivedMemberCount":"3",
  "retirementPlace":"California",
  "fromSource":"https://www.sample.com/path/"
}
```
> Output JSON:

```json
{
  "age": 70,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
	"expectedYearsInHomeCare": 4,
	"exerciserNonSmokerMaxCareCost": 665372.2286233829,
	"nonSmokerMaxCareCost": 764873.6930477947,
	"exerciserNonSmokerIdealBmiMaxCareCost": 457324.6166583799,
	"expectedYearsLost": 13,
	"idealBmiRange": [
  	"BMI_19",
  	"BMI_20",
  	"BMI_21",
  	"BMI_22",
  	"BMI_23",
  	"BMI_24",
  	"BMI_25",
  	"BMI_26",
  	"BMI_27",
  	"BMI_28",
  	"BMI_29",
  	"BMI_30",
  	"BMI_31",
  	"BMI_32",
  	"BMI_33",
  	"BMI_34",
  	"BMI_35"
	],
	"homeCareTotalCost": 204113.307495123,
	"nursingHomeTotalCost": 118880.2104,
	"exerciserMaxCareCost": 459471.6922047717,
	"exerciserIdealBmiMaxCareCost": 459471.6922047717,
	"probabilityOfLivingNinetyFive": 0,
	"probabilityOfLivingNinety": 0,
	"activeYearsWithLongLive": 0,
	"expectedTotalHealthyYears": -3,
	"lifeStyleDisabilityYears": {
  	"exerciserNonSmokerIdealBmi": 4.022322493000001,
  	"idealBmi": 3,
  	"exerciser": 3.6750001907348633,
  	"nonSmokerIdealBmi": 6.022322493000001,
  	"exerciserNonSmoker": 6.022322493000001,
  	"exerciserIdealBmi": 3.6750001907348633,
  	"nonSmoker": 7.022322493000001
	},
	"expectedYearsInAssessedLiving": 2,
	"assessedLivingTotalCost": 97440,
	"calculatedBMI": 31,
	"yearlyCareCostByState": {
  	"homemakerYearlyHealthAideCost": 54912,
  	"homemakerServicesTotalCost": 106818.6,
  	"homemakerServicesYearlyCost": 52620,
  	"assistedLivingYearlyPrivateRoomCost": 48000,
  	"maxCareCost": 227473.68,
  	"nursingHomeSemiYearlyPrivateRoomCost": 91248,
  	"adultDayHealthTotalCareCost": 40632.479999999996,
  	"nursingHomeTotalPrivateRoomCost": 227473.68,
  	"homemakerTotalHealthAideCost": 111471.36,
  	"nursingHomeSemiTotalPrivateRoomCost": 185233.44,
  	"adultDayHealthYearlyCareCost": 20016,
  	"minCareCost": 40632.479999999996,
  	"assistedLivingTotalPrivateRoomCost": 97440,
  	"nursingHomeYearlyPrivateRoomCost": 112056
	},
	"expectedDisabilityYears": 3,
	"diseaseRecommentation": {
  	"Stroke": [
    	"Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
    	"Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
    	"Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
  	],
  	"Alzheimers Disease": [
    	"Engage in social and intellectually stimulating activities",
    	"Exercise regularly and eat a healthy diet rich in fruits and vegetables",
    	"Maintain a healthy weight and get treatment for depression (if applicable)"
  	],
  	"Type 2 Diabetes": [
    	"Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
    	"Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
    	"Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
  	],
  	"Heart Disease": [
    	"Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
    	"Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
    	"Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
  	]
	},
	"probabilityOfLivingHundred": 1.7,
	"idealBmiMaxCareCost": 227473.68,
	"nonSmokerIdealBmiMaxCareCost": 665372.2286233829,
	"lifeStyleYearsLost": {
  	"exerciserNonSmokerIdealBmi": 0,
  	"idealBmi": 13,
  	"exerciser": 10,
  	"nonSmokerIdealBmi": 3,
  	"exerciserNonSmoker": 0,
  	"exerciserIdealBmi": 10,
  	"nonSmoker": 3
	},
	"expectedYearsInNursingHome": 1,
	"totalCareCost": 420433.517895123
  },
  "cancerTypes": [],
  "longLivedMemberCount": 3,
  "states": [],
  "retirementPlace": "California",
  "ethnicity": {
	"European ancestry": 50,
	"African ancestry": 25,
	"Asian ancestry": 25,
	"Hispanic ancestry": 0,
	"Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To get the support care cost and the yearly care cost for the person's disability years.

### Total Out Of Packet Care Cost, Retirement Out Of Packet Care Cost

> Input JSON:

```json
{
  "gender":"male",
  "age":"70",
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "isExercise":false,
  "isSmoker":true,
  "weight":185,
  "height":65,
  "ethnicity":{
 	"European ancestry":50,
 	"African ancestry":25,
 	"Asian ancestry":25,
 	"Hispanic ancestry":0,
 	"Other ancestry":0
  },
  "longLivedMemberCount":"3",
  "retirementPlace":"California",
  "doctorVisitFrequency":"average",
  "retirementAge":"65",
  "fromSource":"https://www.sample.com/path/"
}
```

> Output JSON:

```json
{
  "age": 70,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
	"lifeStyleImpactRetirementAge": {
  	"exerciserNonSmokerIdealBmi": 10,
  	"idealBmi": -4,
  	"exerciser": -3,
  	"nonSmokerIdealBmi": 5,
  	"exerciserNonSmoker": 8,
  	"exerciserIdealBmi": -2,
  	"nonSmoker": 4
	},
	"expectedHealthyYears": 0,
	"expectedYearsInHomeCare": 4,
	"activeRetirementAge": 0,
	"exerciserNonSmokerMaxCareCost": 665372.2286233829,
	"nonSmokerMaxCareCost": 764873.6930477947,
	"exerciserNonSmokerIdealBmiMaxCareCost": 457324.6166583799,
	"expectedYearsLost": 13,
	"idealBmiRange": [
  	"BMI_19",
  	"BMI_20",
  	"BMI_21",
  	"BMI_22",
  	"BMI_23",
  	"BMI_24",
  	"BMI_25",
  	"BMI_26",
  	"BMI_27",
  	"BMI_28",
  	"BMI_29",
  	"BMI_30",
  	"BMI_31",
  	"BMI_32",
  	"BMI_33",
  	"BMI_34",
  	"BMI_35"
	],
	"expectedCareCost": 42884,
	"homeCareTotalCost": 204113.307495123,
	"nursingHomeTotalCost": 118880.2104,
	"lifeStyleImpactCareCost": {
  	"exerciserNonSmokerIdealBmi": 85725,
  	"idealBmi": 21340,
  	"exerciser": 26675,
  	"nonSmokerIdealBmi": 66504,
  	"exerciserNonSmoker": 85725,
  	"exerciserIdealBmi": 26675,
  	"nonSmoker": 66504
	},
	"exerciserMaxCareCost": 459471.6922047717,
	"exerciserIdealBmiMaxCareCost": 459471.6922047717,
	"probabilityOfLivingNinetyFive": 0,
	"probabilityOfLivingNinety": 0,
	"activeYearsWithLongLive": 0,
	"careCostBreakDown": {
  		"belSevenFourAnnual": "$5,335.00",
  		"belSixFourTotal": "$0.00",
  		"belEighteenAnnual": "$1,429.00",
  		"belEightFourAnnual": "$6,407.00",
  		"aboveEightFiveTotal": "$0.00",
  		"belEighteenTotal": "$0.00",
  		"belSevenFourTotal": "$22,319.65",
  		"retirementOutOfPacketCareCost": "$22,319.65",
  		"belSixNineAnnual": "$4,137.00",
  		"belSixNineTotal": "$0.00",
  		"belSevenNineAnnual": "$5,403.00",
  		"belSevenNineTotal": "$0.00",
  		"totalOutOfPacketCareCost": "$22,319.65",
  		"belEightFourTotal": "$0.00",
  		"aboveEightFiveAnnual": "$9,469.00",
  		"belSixFourAnnual": "$1,866.00"
	},
	"expectedTotalHealthyYears": -3,
	"lifeStyleDisabilityYears": {
  	"exerciserNonSmokerIdealBmi": 4.022322493000001,
  	"idealBmi": 3,
  	"exerciser": 3.6750001907348633,
  	"nonSmokerIdealBmi": 6.022322493000001,
  	"exerciserNonSmoker": 6.022322493000001,
  	"exerciserIdealBmi": 3.6750001907348633,
  	"nonSmoker": 7.022322493000001
	},
	"expectedYearsInAssessedLiving": 2,
	"assessedLivingTotalCost": 97440,
	"calculatedBMI": 31,
	"lifeStyleHealthyYears": {
  	"exerciserNonSmokerIdealBmi": 0,
  	"idealBmi": 0,
  	"exerciser": 0,
  	"nonSmokerIdealBmi": 0,
  	"exerciserNonSmoker": 0,
  	"exerciserIdealBmi": 0,
  	"nonSmoker": 0
	},
	"yearlyCareCostByState": {
  	"homemakerYearlyHealthAideCost": 54912,
  	"homemakerServicesTotalCost": 106818.6,
  	"homemakerServicesYearlyCost": 52620,
  	"assistedLivingYearlyPrivateRoomCost": 48000,
  	"maxCareCost": 227473.68,
  	"nursingHomeSemiYearlyPrivateRoomCost": 91248,
  	"adultDayHealthTotalCareCost": 40632.479999999996,
  	"nursingHomeTotalPrivateRoomCost": 227473.68,
  	"homemakerTotalHealthAideCost": 111471.36,
  	"nursingHomeSemiTotalPrivateRoomCost": 185233.44,
  	"adultDayHealthYearlyCareCost": 20016,
  	"minCareCost": 40632.479999999996,
  	"assistedLivingTotalPrivateRoomCost": 97440,
  	"nursingHomeYearlyPrivateRoomCost": 112056
	},
	"expectedDisabilityYears": 3,
	"diseaseRecommentation": {
  	"Stroke": [
    	"Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
    	"Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
    	"Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
  	],
  	"Alzheimers Disease": [
    	"Engage in social and intellectually stimulating activities",
    	"Exercise regularly and eat a healthy diet rich in fruits and vegetables",
    	"Maintain a healthy weight and get treatment for depression (if applicable)"
  	],
  	"Type 2 Diabetes": [
    	"Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
    	"Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
    	"Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
  	],
  	"Heart Disease": [
    	"Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
    	"Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
    	"Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
  	]
	},
	"probabilityOfLivingHundred": 1.7,
	"idealBmiMaxCareCost": 227473.68,
	"nonSmokerIdealBmiMaxCareCost": 665372.2286233829,
	"lifeStyleYearsLost": {
  	"exerciserNonSmokerIdealBmi": 0,
  	"idealBmi": 13,
  	"exerciser": 10,
  	"nonSmokerIdealBmi": 3,
  	"exerciserNonSmoker": 0,
  	"exerciserIdealBmi": 10,
  	"nonSmoker": 3
	},
	"expectedYearsInNursingHome": 1,
	"totalCareCost": 420433.517895123
  },
  "cancerTypes": [],
  "longLivedMemberCount": 3,
  "doctorVisitFrequency": "average",
  "retirementAge": 65,
  "states": [],
  "retirementPlace": "California",
  "ethnicity": {
	"European ancestry": 50,
	"African ancestry": 25,
	"Asian ancestry": 25,
	"Hispanic ancestry": 0,
	"Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To get the total and retirement Out Of Pocket care cost details.

### Sending Emails
>Input JSON:

```json
{
  "ethnicity":{
     "European ancestry":50,
     "African ancestry":30,
     "Asian ancestry":20,
     "Hispanic ancestry":0,
     "Other ancestry":0
  },
  "gender":"male",
  "age":"70",
  "firstName":"first name",
  "lastName":"last name",
  "email":"sample@domain.com",
  "retirementAge":"65",
  "retirementPlace":"California",
  "longLivedMemberCount":"3",
  "doctorVisitFrequency":"average",
  "isExercise":false,
  "isSmoker":true,
  "havingStroke":true,
  "havingDiabetes":true,
  "havingHeartDisease":true,
  "havingAlzheimer":true,
  "cancerTypes":[
  ],
  "weight":"185",
  "height":65,
  "fromSource":"https://www.sample.com/path/"
}
```
> Output JSON:

```json
{
  "age": 70,
  "gender": "male",
  "fromSource": "https://www.sample.com/path/",
  "firstName": "first name",
  "lastName": "last name",
  "email": "sample@domain.com",
  "height": 65,
  "weight": 185,
  "isExercise": false,
  "isSmoker": true,
  "havingDiabetes": true,
  "havingHeartDisease": true,
  "havingStroke": true,
  "havingAlzheimer": true,
  "results": {
    "lifeStyleImpactRetirementAge": {
      "exerciserNonSmokerIdealBmi": 9,
      "idealBmi": -4,
      "exerciser": -4,
      "nonSmokerIdealBmi": 4,
      "exerciserNonSmoker": 7,
      "exerciserIdealBmi": -3,
      "nonSmoker": 3
    },
    "expectedHealthyYears": 0,
    "expectedYearsInHomeCare": 4,
    "activeRetirementAge": 0,
    "exerciserNonSmokerMaxCareCost": 665372.2286233829,
    "nonSmokerMaxCareCost": 764873.6930477947,
    "exerciserNonSmokerIdealBmiMaxCareCost": 457324.6166583799,
    "expectedYearsLost": 13,
    "idealBmiRange": [
      "BMI_19",
      "BMI_20",
      "BMI_21",
      "BMI_22",
      "BMI_23",
      "BMI_24",
      "BMI_25",
      "BMI_26",
      "BMI_27",
      "BMI_28",
      "BMI_29",
      "BMI_30",
      "BMI_31",
      "BMI_32",
      "BMI_33",
      "BMI_34",
      "BMI_35"
    ],
    "expectedCareCost": 42884,
    "homeCareTotalCost": 204113.307495123,
    "nursingHomeTotalCost": 118880.2104,
    "lifeStyleImpactCareCost": {
      "exerciserNonSmokerIdealBmi": 79318,
      "idealBmi": 21340,
      "exerciser": 21340,
      "nonSmokerIdealBmi": 60097,
      "exerciserNonSmoker": 79318,
      "exerciserIdealBmi": 21340,
      "nonSmoker": 60097
    },
    "exerciserMaxCareCost": 465624.1647687048,
    "exerciserIdealBmiMaxCareCost": 465624.1647687048,
    "probabilityOfLivingNinetyFive": 0,
    "probabilityOfLivingNinety": 0,
    "activeYearsWithLongLive": 0,
    "careCostBreakDown": {
      "belSevenFourAnnual": "$5,335.00",
      "belSixFourTotal": "$0.00",
      "belEighteenAnnual": "$1,429.00",
      "belEightFourAnnual": "$6,407.00",
      "aboveEightFiveTotal": "$0.00",
      "belEighteenTotal": "$0.00",
      "belSevenFourTotal": "$22,319.65",
      "retirementOutOfPacketCareCost": "$22,319.65",
      "belSixNineAnnual": "$4,137.00",
      "belSixNineTotal": "$0.00",
      "belSevenNineAnnual": "$5,403.00",
      "belSevenNineTotal": "$0.00",
      "totalOutOfPacketCareCost": "$22,319.65",
      "belEightFourTotal": "$0.00",
      "aboveEightFiveAnnual": "$9,469.00",
      "belSixFourAnnual": "$1,866.00"
    },
    "expectedTotalHealthyYears": -3,
    "lifeStyleDisabilityYears": {
      "exerciserNonSmokerIdealBmi": 4.022322493000001,
      "idealBmi": 3,
      "exerciser": 3.2300000190734863,
      "nonSmokerIdealBmi": 6.022322493000001,
      "exerciserNonSmoker": 6.022322493000001,
      "exerciserIdealBmi": 3.2300000190734863,
      "nonSmoker": 7.022322493000001
    },
    "expectedYearsInAssessedLiving": 2,
    "assessedLivingTotalCost": 97440,
    "calculatedBMI": 31,
    "lifeStyleHealthyYears": {
      "exerciserNonSmokerIdealBmi": 0.20767704923632735,
      "idealBmi": 0,
      "exerciser": 0.20767752607348555,
      "nonSmokerIdealBmi": 0.20767704923632735,
      "exerciserNonSmoker": 0.20767704923632735,
      "exerciserIdealBmi": 0.20767752607348555,
      "nonSmoker": 0.20767704923632735
    },
    "yearlyCareCostByState": {
      "homemakerYearlyHealthAideCost": 54912,
      "homemakerServicesTotalCost": 106818.6,
      "homemakerServicesYearlyCost": 52620,
      "assistedLivingYearlyPrivateRoomCost": 48000,
      "maxCareCost": 227473.68,
      "nursingHomeSemiYearlyPrivateRoomCost": 91248,
      "adultDayHealthTotalCareCost": 40632.479999999996,
      "nursingHomeTotalPrivateRoomCost": 227473.68,
      "homemakerTotalHealthAideCost": 111471.36,
      "nursingHomeSemiTotalPrivateRoomCost": 185233.44,
      "adultDayHealthYearlyCareCost": 20016,
      "minCareCost": 40632.479999999996,
      "assistedLivingTotalPrivateRoomCost": 97440,
      "nursingHomeYearlyPrivateRoomCost": 112056
    },
    "expectedDisabilityYears": 3,
    "diseaseRecommentation": {
      "Stroke": [
        "Keep your blood pressure in check. Next time you\\'re at the doctor, ask him to check your blood pressure and discuss any lifestyle changes you may need to make.",
        "Do not smoke. If you are currently smoking, talk to your doctor about support programs and ways to quit.",
        "Stay fit. Obesity is associated with an increased risk of stroke, and staying active and fit can reduce your risk."
      ],
      "Alzheimers Disease": [
        "Engage in social and intellectually stimulating activities",
        "Exercise regularly and eat a healthy diet rich in fruits and vegetables",
        "Maintain a healthy weight and get treatment for depression (if applicable)"
      ],
      "Type 2 Diabetes": [
        "Get off the couch! Exercise can help you loose weight and lower your blood sugar.",
        "Increase your fiber intake. Fruits, veggies, whole grains beans, nuts and seeds are great sources.",
        "Talk with your doctor. Since diabetes often goes undiagnosed, it is important to get tested early. Testing is especially important if you are overweight."
      ],
      "Heart Disease": [
        "Do not smoke. Smoking is one of the top risk factors for heart disease. Even occasional or \"social smoking\" can increase your risk.",
        "Get off the couch! Exercise can help you maintain a healthy weight and keep you heart-healthy.",
        "Eat well. Fruits, veggies and whole grains help protect your heart. Try to limit your intake of red meats, deep-fried foods, and baked goodies."
      ]
    },
    "probabilityOfLivingHundred": 1.7,
    "idealBmiMaxCareCost": 227473.68,
    "nonSmokerIdealBmiMaxCareCost": 665372.2286233829,
    "lifeStyleYearsLost": {
      "exerciserNonSmokerIdealBmi": 0,
      "idealBmi": 13,
      "exerciser": 10,
      "nonSmokerIdealBmi": 3,
      "exerciserNonSmoker": 0,
      "exerciserIdealBmi": 10,
      "nonSmoker": 3
    },
    "expectedYearsInNursingHome": 1,
    "totalCareCost": 420433.517895123
  },
  "cancerTypes": [],
  "longLivedMemberCount": 3,
  "doctorVisitFrequency": "average",
  "retirementAge": 65,
  "states": [],
  "retirementPlace": "California",
  "ethnicity": {
    "European ancestry": 50,
    "African ancestry": 30,
    "Asian ancestry": 20,
    "Hispanic ancestry": 0,
    "Other ancestry": 0
  },
  "traversedPages": {},
  "agentDetails": "Chrome 61.0.3163.100 Linux",
  "genivityAdviser": {
	"id": 1,
	"name": "person",
	"email": "person@domain.com",
	"siteUrl": "https://www.sample.com/path/",
	"isActive": 1,
	"address": "5, 2nd Street, Somewhere.",
	"phoneNumber": "0000000000",
	"firmName": "Firm Name"
  }
}
```
To send the genivity calculator reports to the adviser and confirmation mail to the clients.