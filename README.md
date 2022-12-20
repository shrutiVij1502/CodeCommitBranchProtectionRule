# Code Commit Branch Protection Rule

## Create a code commit repository and then create a new branch where developer can make their changes and can create a pull request

<img width="824" alt="image" src="https://user-images.githubusercontent.com/67600604/208613711-027c1434-d100-4d26-92d5-eb7593c98799.png">

## Then go to this option to create a request approval.

<img width="530" alt="image" src="https://user-images.githubusercontent.com/67600604/208613917-edf4f1ad-d509-4183-8557-cbb8c1f45774.png">

## Create a template - 

<img width="659" alt="image" src="https://user-images.githubusercontent.com/67600604/208614099-4d4d68e7-1c9e-4197-97b6-d75645ca891c.png">

## Now make changes in the Branch and create the PR
It will ask Shruti.Vij IAM user to review and approve the changes.

- Approve the request 

``` Note - You can not approve your own created PR. ```

### Security Policy to restrict the Actions on the Specified Branches

## Create a IAM policy and attach it to the user , you want to restrict the actions.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "codecommit:GitPush",
                "codecommit:DeleteBranch",
                "codecommit:PutFile",
                "codecommit:MergeBranchesByFastForward",
                "codecommit:MergeBranchesBySquash",
                "codecommit:MergeBranchesByThreeWay",
                "codecommit:MergePullRequestByFastForward",
                "codecommit:MergePullRequestBySquash",
                "codecommit:MergePullRequestByThreeWay"
            ],
            "Resource": "<REPO-ARN>",
            "Condition": {
                "StringEqualsIfExists": {
                    "codecommit:References": [
                        "refs/heads/main",
                        "refs/heads/uat",
                        "refs/heads/prod"
                    ]
                },
                "Null": {
                    "codecommit:References": false
                }
            }
        }
    ]
}
```
It will restrict the user to perform these actions.

