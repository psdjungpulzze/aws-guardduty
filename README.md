# Summary
Extract data from AWS Guard Duty

# API AutoFlow Version:
Configuration config.json was created using AutoFlow version __0.2.5__# Storing data:

# Need help?
Is you have questions about this example, feel free to post your question on the community "<a href="https://interactor.com/autoflow/questions" target="_blank">Ask Questions</a>" website.

# Extracting data from AWS Guard Duty:

## Step 1. Create flow
* Create an HTTP Server
* Create an endpoint
  * NOTE: under properties the method must be GET
* From the right panel, press Action tab -> Service -> Aws, Drag and drop action __REST__ to the end of the flow
* From the right panel, press Action tab -> Service -> Aws, drag and drop another action __REST__ to the end of the flow
* From the right panel, press Action tab -> json, Drag and drop decode to the end of the flow

## Step 2. Get Guard Duty Issues List
### Service/Aws/Rest Action
This action extracts just the issues list from AWS Guard Duty by using the API /detector/_detector_id_/findings

#### Properties:
> * service:          _guardduty_
> * method:           _POST_
> * path:             _/detector/your-detectorId/findings_
> * action:   
> * parameters:
> * body:
> * string
> * region:           _us-west-2_
> * access-key-id:    _your-aws-secret-access-key_
> * secret-access-key: _your-aws-access-key-id_
> * se-mock-result:
> * mock-result:

#### Output:
> * output-location:   _result_

_How to get access-key-id and secret-access-key_
https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/

_Guard Duity Actions_
https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFindings.html

## Step 3. Get Guard Duty Issues Lists
Using the Guard Duty issues list from the previous step, this action retrieves the details of each issue by using the API /detector/_detector_id_/findings/GET.
Note that this API takes in the issues list in the request body (which was obtain from previous action).
The output is stored back into the variable result.

> * service:          _guardduty_
> * method:           _POST_
> * path:             _/detector/your-detectorId/findings/get_
> * action:   
> * parameters:
> * body:             [R][S] _result_
> * string
> * region:           _us-west-2_
> * access-key-id:    _your-aws-secret-access-key_
> * secret-access-key: _your-aws-access-key-id_
> * se-mock-result:
> * mock-result:

#### Output:
> * output-location:   _result_


## Step 4. Decode Data for easier access
### Json/decode
#### Properties:
> * json: drag drop the __result body__ from right data panel

#### Output:
> * At-location: drag and drop the __response__ body from the right panel


## AWS Guard Duty API reference

https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFindings.html
