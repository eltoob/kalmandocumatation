---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - swift
  - objective_c
  - java
  - csharp

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

# includes:
#   - errors

search: true
---

# Introduction

Welcome to Kalman Analytics API. Your can use this API to access Kalman endpoints and feed data to consult and analyse in your analytics dashboard.

We have language bindings in Objective-C, Swift, Java, and CSharp! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.
Contact support@kalmanlabs.com for more details if you need help setting up your specific project.


# Configuration

> To instantiate the SDK, use this code:

```objective_c
// Create a Kalman instance
Kalman *kalman = [Kalman sharedInstanceWithToken:@"MY_API_KEY" 
  AppID:@"MY_APP_ID"];
```

```swift
Kalman.initialize(token: "MY_API_KEY", appID: "MY_APP_ID)
```

```java
// 
// Initialize the library with your Kalman project token,
// MY_API_KEY, your API Key, MY_APP_ID and a reference to your
// application context.
Kalman kalman =
    Kalman.getInstance(context, MY_APP_ID, MY_API_KEY);
```

> Make sure to replace `MY_API_KEY` with your API key and `MY_APP_ID`.

Kalman Analytics uses API keys and APP ID to allow access to the API. You can register a new Kalman API key at our [developer portal](http://kalmanlabs.com/developers).

# User Tracking

```objective_c
// Set customer User ID. Note that if this is not set, a random user uuid will be generated for your player
[kalman configureUserId:@"123"];
[kalman.user set:@{@"channel": @"campaign_32"}];
```

```swift
kalman.configureUserId(userID: "1")
kalman.registerSuperProperties(["channel": "campaign_32"])
```

```java
kalman.configureUserId(userID: "1")
JSONObject props = new JSONObject();
props.put("channel", "campaign_32");
kalman.registerSuperProperties(props);
```

Kalman SDK allows you to set user level configuration. This is could used to capture channel of acquisition or some in game characteristics.
> Note that if no userID is set, the user is automatically assigned a uuid.

<aside class="notice">
You must replace <code>MY_API_KEY</code> and <code>MY_APP_ID</code> with your API key and APP ID.
</aside>

# Track Event
## Track Purchase Event
```objective_c
Kalman *kalman = [Kalman sharedInstance];
[kalman trackPurchaseWithCurrency:@"USD" 
  amount:999
  itemID:@"gems"
  quantity:20];
```

```swift
Kalman.trackPurchase(
  currency: "USD", 
  amount: 999,
  itemID: "gems",
  quantity: 20
)
```

```java
kalman.trackPurchase(
  "USD", 
  999,
  "gems",
  20
)
```
Purchase events are used to track information related to monetization of the app.
When recording a purchase event. You will need to specify the following fields

Field | Type | Required | Example | Meaning
----- | ---- | -------- | ------- | -------
name | string | optional | 50 Gems | Name of the object acquired
currency | string | Optional(default: USD) | USD | Describes the currency using ISO 4217
itemID | string | optional | gem | Represents the item bought
quantity | integer | optional | 50 | the quantity of an item bought
## Track Ads Event Event
```objective_c
Kalman *kalman = [Kalman sharedInstance];
[kalman trackAdsEventWitType:@"rewarded_video"
   adProvider:@"unity"];
```

```swift
Kalman.trackAdsEvent(
  type: "rewarded_video", 
  adProvider: "unity"
)
```
```java
kalman.trackAdsEvent(
  "rewarded_video",
  "unity"
)
```
Purchase events are used to track information related to monetization of the app.
When recording a purchase event. You will need to specify the following fields

Field | Type | Required | Example | Meaning
----- | ---- | -------- | ------- | -------
adType | string | required | 'rewarded_ads' | Name of the type of ads
adProvider | string | optional | 'unity' | name of the ads supplier
metadata | Object | optional |  | can be used to store any type of metadata

## Track Level Progression Event
```objective_c
Kalman *kalman = [Kalman sharedInstance];
[kalman trackProgressionEventWithLevel:@"level_01_03"
   status:@"finished"];
```

``` swift
Kalman.trackProgressionEventWithLevel(
  level: "level_01_03", 
  status: "finished"
)
```

```java
Kalman.trackProgressionEvent(
  "level_01_03", 
  "finished"
)
```
Field | Type | Required | Example | Meaning
----- | ---- | -------- | ------- | -------
level | string | required | 'level1' | describes the level completion
status | string | required | 'finished' | described the status of a level (started, finished)

## Track Custom Event
```objective_c
Kalman *kalman = [Kalman sharedInstance];
[kalman trackWithEvent:@"Some Event" metadata:@{
    @"someProperties": @"Test"
}];
```

```swift
kalman.track(event: "SomeEvent",
  metadata: ["someProperties" : "Test"])
```

```java
JSONObject metadata = new JSONObject();
props.put("channel", "campaign_32");
kalman.track("SomeEvent",
  metadata)
```
Field | Type | Required | Example | Meaning
----- | ---- | -------- | ------- | -------
event | string | required | 'event1' | describes the event you want to track.
metadata |  Object | optional |  | can be used to store any type of metadata