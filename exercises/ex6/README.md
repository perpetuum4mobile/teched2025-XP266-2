# Exercise 6 - Manage your Feature in Cloud ALM & Deployment

In this exercise, we will manage the assignment and deployment of Cloud Transport Management service transport requests in SAP Cloud ALM. By managing the lifecycle of your Feature you can keep track of your changes with a governed process. This includes confirmation of successful test in QA and the apporval for the deployment to the production environment. Eventually you can validate the deployed application in the production environment.

## Exercise 6.0 - Manage the lifefcylce of your feature

1. Go to the **Features** application in [SAP Cloud ALM](https://xp266-calm-lf1zy9xc.eu10-004.alm.cloud.sap/launchpad#Shell-home).
2. Go to **your Feature** created in Exercise 2.

    <br>![alt text](../ex6/images/feature_in_overview.png)
3. Switch to **Edit** mode.

    <br>![alt text](../ex6/images/feature_edit.png)
4. Go to the **Transports** section and click **"Assign"**.

    <br>![alt text](../ex6/images/transport_assign.png)
5. In the selection dialog search for **your transport IDs** (prefix is the destination name of the connection between Cloud ALM and CTMS).

    <br>![alt text](../ex6/images/transport_search.png)
6. Select both transports - the one for your UI5 app and the one for Mobile Services - and click "Assign".

    <br>![alt text](../ex6/images/transport_select.png)
7. Save and Close the Feature.
8. The Transports are assigned to your Feature.

    <br>![alt text](../ex6/images/transport_assigned.png)

   
## Exercise 6.1 - Deploy and monitor changes in your QA and Prod environment

1. The **transports in the Transports** section is **released** and show the **CTMS target nodes** as target tenants.

    <br>![alt text](../ex6/images/transport_status_target.png)
2. Click **"Deploy"** and confirm the deployment to the target nodes in the dialog.

    <br>![alt text](../ex6/images/trigger_deploy_QA.png)

    <br>![alt text](../ex6/images/confirm_deploy_QA.png)
3. The Status of the transports is changed to "Deployment Scheduled in QA"

     <br>![alt text](../ex6/images/deployment_scheduled_QA.png)
4. Use the **Refresh button** on the Transports Section **to retrieve the import results**.

    <br>![alt text](../ex6/images/refresh_QA.png)
4. As soon as the imports have been succesful the **status changes to "Deployed in QA"**.
5. Now you can **change the Feature status to "In Testing"** by clicking **"Handover to Test"**.

    <br>![alt text](../ex6/images/handover_test.png)
6. The action "Confirm Successful Test" will be **executed centrally**.
7. Click on **"Analytics"** in the top right corner to **access the Feature Traceability**.

    <br>![alt text](../ex6/images/feature_traceability_nav.png)
8. Check whether your feature is in **status "Successfully Tested"**.
9. Now you can **approve the Feature for Production** by clicking "Approve for Production".
10. In status "Approved for Production" you can **trigger the deployment to production by clicking "Deploy"** in the Transports section.
11. Refresh the section to retrieve the import results.

## Exercise 6.2 - Find and access the deployed applications

After completing these steps you will have...

## Summary

You've now done
