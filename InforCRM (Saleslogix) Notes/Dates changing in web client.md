## Infor CRM UTC Time changing dates in web client

#### About:  Infor CRM converts dates to their UTC (Timezone) equivalent when displaying them in the web form.  Dates imported from other systems with a time of 00:00:00 can be problematic.  Eastern time is -5 and when a 00:00:00 time is displayed in the ICRM web client it renders as the prior days date.

##### Symptom:  Infor CRM (Saleslogix) is changing dates to yesterday in the web form but when I check the database they look fine

#### To get around this quickly (and because we aren't using time on these fields) the following query adds 10 hours to the date.  This is enough to cover users in the US.

``` SQL

--Get a count of the records to be modified (Optional)
SELECT COUNT(*)
from sysdba.TEST_OPPORTUNITY_UDF udf
where commitdate is not null
and cast(commitdate as time) = '00:00:00'
 
--Make a copy of the table for testing later (Optional)
SELECT * INTO BBB_UDF_TEST
FROM sysdba.TEST_OPPORTUNITY_UDF

--The script that does the work UPDATE 1849 ROWS
update udf
set commitdate = dateadd(hour, 10, commitdate)
from sysdba.TEST_OPPORTUNITY_UDF udf
where commitdate is not null
and cast(commitdate as time) = '00:00:00'
 
--VERIFY THERE ARE NO ISSUES BY COMPARING TO TABLE COPY (Optional)
select udf.commitdate, ut.commitdate, cast(udf.commitdate as date) [date], cast(ut.commitdate as date) [date]
from sysdba.TEST_OPPORTUNITY_UDF udf
join BBB_UDF_TEST ut
on ut.proposalid = udf.proposalid
where udf.commitdate is not null
and cast(udf.commitdate as time) = '00:00:00'
and cast(udf.commitdate as date) <> cast(ut.commitdate as date)

```