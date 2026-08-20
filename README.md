# Olympics DCM Project Demo

A demo of Snowflake's **DCM Projects** (Database Change Management) — a declarative, infrastructure-as-code way to manage Snowflake database objects, similar to Terraform. Instead of writing `CREATE`/`ALTER` statements by hand, you declare the desired state of your objects in definition files, and Snowflake computes and applies the diff via a plan-then-deploy workflow.

This project declares and deploys a warehouse and a table (schema based on my [Olympic Historical Analyst](https://github.com/) project) to demonstrate the workflow.

## How to run it

1. In `manifest.yml`, replace `<your-account-identifier>` with your own Snowflake account identifier:
   ```sql
   SELECT CURRENT_ORGANIZATION_NAME() || '-' || CURRENT_ACCOUNT_NAME();
   ```

2. Open `Run_file.sql` in a Snowsight worksheet.

3. Run the setup statements at the top (`USE ROLE`, create database/schema, create the DCM project, create the stage).

4. Upload `manifest.yml` and the `sources/definitions/` folder (keep the folder structure intact) to the stage: **Data → Databases → OLYMPICS_ANALYTICS_DEV → CORE → Stages → dcm_stage → + Files**.

5. Run `LIST @OLYMPICS_ANALYTICS_DEV.CORE.dcm_stage;` to confirm the files landed correctly.

6. Run the **PLAN** statement - a dry run that previews what would be created, with no changes applied.

7. Run the **DEPLOY** statement — applies the changes for real.

8. Run the two `SHOW` statements at the bottom to confirm `ATHLETE_EVENTS` and `OLYMPICS_WH` now exist.
