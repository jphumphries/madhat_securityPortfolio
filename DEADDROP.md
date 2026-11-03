
# Operation Dead Deploy: Resource Group Policy Oversight

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


<img width="1425" height="968" alt="01_Find Resource Group" src="https://github.com/user-attachments/assets/2e87fb1a-ba4a-4b39-9949-49782adc6350" /> 


3. Inside the target resource group is found the one resource that the intern deployed 


<img width="1055" height="836" alt="02_Inside Resource Group" src="https://github.com/user-attachments/assets/e854e09b-8ad5-496f-a87f-255c36759386" /> 


4. Here we take a look at the tags and find documentation that gives us bread crumbs to what happened during this incident. 


<img width="1633" height="736" alt="03_RG Tags" src="https://github.com/user-attachments/assets/04c7ef7e-0fc8-4d34-8987-6b897c650576" /> 


5. Moving back out to the resource group blade, and navigating the policies blade we can take a look at the policy that failed to prevent this incident 


<img width="1058" height="836" alt="04_Resource Group Deployments" src="https://github.com/user-attachments/assets/6c948da6-0aec-424c-8342-31a776c55742" /> 


6. Going from Policies > Naming Convention we see that the effect type is Audit which only logs what occurs within the resource group in terms of naming but does nothing to enforce compliance through denial of improper resource and deployment naming. 


<img width="1637" height="658" alt="05_Policy List" src="https://github.com/user-attachments/assets/05df1fd4-a679-476f-929a-e14a5ca67c70" /> 
Policy List


<img width="1615" height="754" alt="06_Inside The Policy Details" src="https://github.com/user-attachments/assets/7fbeb41d-0d11-46de-8922-ae2b71afe64d" /> 
Policy Details


<img width="1615" height="579" alt="07_Effect Type Audit" src="https://github.com/user-attachments/assets/9d244e87-a84e-487e-a221-8e9e8cc47736" /> 
Policy Effect


7. If there had been no prior knowledge of the actions of the intern this discrepancy may have gone unnoticed and caused a problem later when another less visible associate broke the naming convention

## What broke / what surprised me
This scenario is a lesson in always examining and customizing your settings when setting up a new system. In this case, that being a resource group within Azure.

Being new to Azure, it took some time getting used to the environment and what seems like regular repetition of information on different blades. In other words, navigation is a bit unwieldy at first. I’m somewhat overwhelmed with how many sets of information are nested within certain blades.

Leaving the default settings (or policy effects) in place could have had devastating effects had this not been a simple intern without much knowledge about what they were doing. A threat actor could make use of the convention breaking resource to breach the system. A simple default policy effect, “audit”, was the difference between compliance and a potential breach or sitting resource group

The resource that was set up could have had cost implications for the business, even if space for the temporary resource was alloted at the beginning.


## Findings and recommendations
The default settings need to be adjusted to the policy on hand. Ever policy and effect must be examined to ensure compliance thus disallowing there sorts of errors. 

My initial recommendation is to change the policy effect to deny, however if it were possible to put a time limit of the life of the deployed resource by the intern I might suggest modifying the resource upon creation so that it falls in line with conventions, serves it’s purpose for the intern, and is promptly discarded when not in use anymore.

To put it simply:

1. Change Default Policy Effects (From Audit > Deny)
2. Confirm that the intern’s access is properly limited to prevent the creation of standing RGs and resources in unnecessary regions
3. Confirm that the intern’s temporary access expires when appropriate
4. Educate employees at onboarding and periodically about implemented policies and procedures.


## What I learned
- While I’d like to magically be able to navigate this platform well, it will take time to know exactly what I need to look for and where. I’m patient to understand what I should be doing.
- In the future, I need to explore the available blades more to understand the thought process behind where things are placed so I can better trace details.
- Exploring JSON code is also on my list of “things to know how” so that I have another more concrete avenue into understanding policy
