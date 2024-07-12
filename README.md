In field of data warehouse we might seen the scenario where we need to preserve the history of deleled and updated records.\
SCD type 1: In SCD type 1 if new record will come we will insert it into target table, if same records will come with updated value then we will update that records in target              table\
SCD type 2: come into the picture when we want to preserve the history at row level(for all the columns).\
  ->It will consume more storage space as it is maintaining all the history of given PK combination.\
  ->Here we need to add some audit column for tracking purpose, start_dt, end_dt, active_flg\
  ->table structure look like, **emp_id    emp_name    salary    designation    start_dt    end_dt    active_flg**\
SCD type 3: come into the picture when we want to preserve the history for the specific columns.\
  -> For SCD type 3 allow us to keep how many past version of column, we want in table(till 1st past record, or till 2nd past records ...).\
  -> table structure look like,  **emp_id    emp_name   salary    designation    prevsalary_1st    prevsalary_2st** 

********************************************************************************************************************************************************
following steps invovle in our code, please see the code attched in main branch\
Step1: handle SCD type 2 using Snowflake we will create stream on the top of stg table so all the delta will get capture in stream object.\
Step 2: we also create column in target tagble that hold unique value, using the sequenece in Snowflake, later we will use this column in merge statement while updating the records.\
Step 3: we also create the view on top of stream object, in view definition we will mention the logic to calculate the DML_TYPE (which row in stream should have 'I', which should have 'U' and 'D' flag)\
Step 4: Finally we will use the merge statement with view and target table to update and insert the records.\
Step 5: later to automate the script execution, we can create the task and and using CRON we can mention the schedule timing. example: schedule= 'USING CRON 60 * * * MON-FRI Asia/Kolkata'\

![image](https://github.com/user-attachments/assets/f4bcb11f-021f-4706-9bfe-641757c60e56)



