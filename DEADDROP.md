# [Title, outcome-flavored: "Investigating an Identity Attack in Entra ID"]

## Scenario
Madhat Labs Junior Intern used temporary contributor access credentials to create a “test environment” for the sake of a leadership presentation. 
The intern was not informed on policy in regards to proper naming conventions and was able to launch an environment that did not fall within intended boundaries. A policy oversight allowed this user to cut corners our engineers were unaware of.

## Environment
Live Multi-User Azure Training Tenant, Reader Access:
- Madhat Labs Subscription Environment
- Blade navigation to resource group, deployments blade, policy blade, etc.

## Investigation
1. Signed into Azure Madhat subscription
2. Navigated to the resource group within the subscription that does not follow the proper naming convention. The established naming convention made spotting the culprit an exercise in process of elimination by sight. Also could have used the search filter if there were an excessive amount of resource groups to search through

![naming_discrepency](/evidence/w1_naming_discrepency.png)

4. Inside the target resource group is found the one resource that the intern deployed
5. Here we take a look at the tags and find documentation that gives us bread crumbs to what happened during this incident.
6. Moving back out to the resource group blade, and navigating the policies blade we can take a look at the policy that failed to prevent this incident
7. Going from Policies > Naming Convention we see that the effect type is Audit which only logs what occurs within the resource group in terms of naming but does nothing to enforce compliance through denial of improper resource and deployment naming.
8. If there had been no prior knowledge of the actions of the intern this discrepancy may have gone unnoticed and caused a problem later when another less visible associate broke the naming convention

## What broke / what surprised me
The most credible section in the document. Dead ends, wrong guesses, the thing that took an hour. Employers know real work is messy. This section separates you from certificate collectors.

## Findings and recommendations
What you determined, plus 2 or 3 recommendations as if you were reporting to the resource owner.

## What I learned
3 to 5 bullets. At least one technical, one "what I'd do differently."
