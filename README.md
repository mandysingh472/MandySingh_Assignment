
Task Details

Task 1 |  Lead Qualification Validation (Implement a trigger to validate leads before they are converted to opportunities. The trigger should enforce certain criteria for lead qualification, such as ensuring that the lead has a valid email address and phone number, and that key fields are not left blank.)

Design Decisions  
i.	There is simple requirement to check blank fields and field format which can be easily achieved with  Validation rules.
ii.	The reason behind not choosing the Trigger is same that if anything is achievable without code, we should not write code for the same. 
 Assumptions 
i.	We need to stop the lead conversion if few major fields are left blank in the Lead record. In my case, considered Email, Phone and Lead Source for the same.
ii.	We also need to stop the lead conversion if email or phone is in incorrect format. phone format can differ as per region/org requirement. Assumed, US format for this assessment.
iii.	There is standard email format check on the lead page, tested the same and it is working fine as expected. 
iv.	validation will only fire when the lead is being converted and not on the already converted lead update(with special permissions).
 Limitations 
i.	If there are more complex requirements during lead conversion, it would need to be implemented via Apex.
Technical Components:
i.	Validation Rules on Lead Object:
⦁	Check_blank_fields
⦁	Check_Phone_format 



Task 2 | Opportunity Stage Update(Develop a trigger that automatically updates the Opportunity stage based on predefined criteria. For example, if the expected close date is within the next 30 days and the opportunity amount exceeds a certain threshold, the stage should be updated to "Closing.")

Design Decisions 
i.	The requirement is to check all the Opportunities where in close date is within next 30 days, this could not be achieved via Trigger as there won't be any event fired in case there is any opportunity wherein this criteria is meeting but there is no update being done. Thus, Trigger won't fire on idle Opportunities and status will not turn to 'Closing' eventually.
ii.	Thus, created Batch class which can run on the daily basis and identify the opportunities meeting the given criteria and perform appropriate actions.
iii.	Implemented Schedulable Interface as well which will help in scheduling the batch job on the daily basis.
iv.	Created Test class in order to test and complete code coverage for  Batch and Schedulable job.
v.	Created custom label to store Threshold Amount to make it configurable and changed easily as per the bussiness need.If there is any general hierarchical  custom settings to store all system config, that would be more apt to leverage.
 Assumptions 
i.	Going with the assumption that there will be one-time data update activity in order to update historical data meeting the given criteria before batch is deployed to production. This will avoid all the accessive load/governor limits on the batch when it will be executed for the first time.
ii.	Included batch execution date as well in the next 30 days duration. 
iii.	Developed with the assumption that given bussiness requirements should be implemented with the best possible technical approach and not necessaraly as given in the assessment.
 Limitations 
i.	Scheduled jobs are not real time but near to real time.
ii.	Debugging can be bit of a challenge, might require custom logging.
Technical Components:
i.	Batch job Name: OpportunityClosingBatch 
ii.	Test Class Name: OpportunityClosingBatchTest
iii.	Custom label: Threshold_Amount





