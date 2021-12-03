# 💀 Demo Reaper 💀

Keeps your Azure subscription clear of expired resources

## Do you ...

* frequently spin up demo environments in Azure to showcase some particular functionality?
* forget to remove them, wasting both energy and money?

Me too.

## Introducing the Demo Reaper

The reaper will monitor your subscription and automatically end the life your demo resources without you having to take any action

Sound useful? 

## How to onboard your subscription

1. [Use this repository as a template](https://github.com/jasoncabot-ms/demo_reaper/generate)
1. [Configure Azure credentials as GitHub Secret](https://github.com/marketplace/actions/azure-cli-action#configure-azure-credentials-as-github-secret)
   1. Open the [Azure Shell](https://shell.azure.com)
   1. **Run** `az ad sp create-for-rbac --sdk-auth --role contributor`
   1. Go to GitHub -> Settings -> Secrets -> Actions
   1. Add a **Repository Secret** with name `AZURE_CREDENTIALS` with a value of the output you generated earlier
3. ???
4. Profit

## How does it work?

Any resource group created with `delete` in it's name will be culled 7 days after it was created without you having to take any manual action

A GitHub Action, with access to your subscription, will run every day and look for any resources that are past their expiry date. If it finds any, they will be culled.

## Can I change how long a resource group will be considered valid?

Yes - just add a tag called `delete` with an integer value for the number of days this resource group should be active.

For example this resource group called `app-service-delete` with tag `{delete: 3}` will be culled automatically **3 days** after it was created.

![image](https://user-images.githubusercontent.com/51163690/144624751-f58592ef-ebf7-48e6-9ac3-ff507a268732.png)
![image](https://user-images.githubusercontent.com/51163690/144624790-3b907be8-512a-42b7-a0eb-fd38c2a4b64d.png)

## How do I know if it worked?

Look in the GitHub actions log. A run where expired resources were found would look something like this:

![image](https://user-images.githubusercontent.com/51163690/144629997-fae8b5f6-a6cb-49f2-a655-dba87070c54b.png)

Otherwise if no expired resources were found, then something like this:

![image](https://user-images.githubusercontent.com/51163690/144630179-0e6e35dc-51c7-4e9a-b71f-557fd57a0c20.png)


## How to run locally

```bash
SUBSCRIPTION_ID=... node reap
```
