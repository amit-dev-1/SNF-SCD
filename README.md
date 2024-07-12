In field of data warehouse we might seen the scenario where we need to preserve the history of deleled and updated records.
SCD type 1: In SCD type 1 if new record will come we will insert it into target table, if same records will come with updated value then we will update that records in target              table
SCD type 2: come into the picture when we want to preserve the history at row level(for all the columns).
  ->It will consume more storage space as it is maintaining all the history of given PK combination.
  ->Here we need to add some audit column for tracking purpose, start_dt, end_dt, active_flg
  ->table structure look like, **emp_id    emp_name    salary    designation    start_dt    end_dt    active_flg**
SCD type 3: come into the picture when we want to preserve the history for the specific columns.
  -> For SCD type 3 allow us to keep how many past version of column, we want in table(till 1st past record, or till 2nd past records ...).
  -> table structure look like,  **emp_id    emp_name   salary    designation    prevsalary_1st    prevsalary_2st** 

********************************************************************************************************************************************************



