![Grim Reaper Illustration](https://user-images.githubusercontent.com/51163690/144595058-d635dc36-97c0-40a4-88ef-75c4efeb9417.jpg)

## Do you ...

* frequently spin up demo environments in Azure to showcase some particular functionality?
* forget to remove them, wasting both energy and money?

Me too.

## Introducing the Demo Reaper

The reaper will monitor your subscription and automatically end the life your demo resources without you having to take any action

Sound useful? 

## How to onboard your subscription

1. Use this repository as a template
1. [Configure Azure credentials as GitHub Secret](https://github.com/marketplace/actions/azure-cli-action#configure-azure-credentials-as-github-secret)
1. ???
1. Profit

## How does it work?

Any resource group created with `delete` in it's name will be culled 7 days after it was created without you having to take any manual action.

## Can I change how long a resource group will be considered valid?

Yes - just add a tag called `delete` with an integer value for the number of days this resource group should be active.

For example this resource group called `app-service-delete` with tag `{delete: 3}` will be culled automatically **3 days** after it was created.

![image](https://user-images.githubusercontent.com/51163690/144624751-f58592ef-ebf7-48e6-9ac3-ff507a268732.png)
![image](https://user-images.githubusercontent.com/51163690/144624790-3b907be8-512a-42b7-a0eb-fd38c2a4b64d.png)

## How to run locally

```bash
SUBSCRIPTION_ID=... node reap
```
