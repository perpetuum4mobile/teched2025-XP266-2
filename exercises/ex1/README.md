## Exercise 1 - Setup your Delivery Pipeline and Transport Landscape

In this exercise, you will define your delivery pipeline in SAP Continuous Integration and Delivery service, create a job and configure the release step and transport landscape in SAP Cloud Transport Management Service.

# Exercise 1.0 - Open the Continuous Integration and Delivery Service

1. In your SAP BTP subaccount named with **XP266_CENTRAl**, go to **Services -> Instances and Subscription**.
2. In the **Subscriptions** overview, choose **Continuous Integration & Delivery**. Now, the user interface of SAP Continuous Integration and Delivery opens.
    <br>![](../ex1/images/sub_cicd.png)

## Exercise 1.1 - Add Your Repository in SAP CI CD Service

Connect SAP Continuous Integration and Delivery with the repository in which your sources reside.

1. In SAP Continuous Integration and Delivery, choose Repositories → **+** (Add).
    <br>![](../ex1/images/repo_cicd.png)

1. In the Add Repository column view, add a **name** e.g. `teched-repo`

2. In GitHub, copy the HTTPS clone URL of the repository you just created in [Exercise 0](../ex0#exercicse-01---create-a-copy-of-this-repository) 
    <br>![](../ex1/images/copy_git_repo.png)

3. Paste it into the Clone URL field in the Add Repository column view.
    <br>![](../ex1/images/add_repo_view.png)

4. Don't close the repo-creation yet. In the next step we will add a GitHub webhook

## Exercise 1.2 - Create a Webhook

You can configure a webhook for your repository, which automatically triggers a build of your job once there is a change commit in the source code repository.

1. In the same view, click the button to create a new webhook credential.
    <br>![](../ex1/images/add_webhook.png)

2. In the new popup, click the **+** button to create a new webhook credential.
    <br>![](../ex1/images/create_webhook_credential.png)

3. Another Create Credential popup opens. Here, choose a name e.g. `webhook-credential`.
4. Generate a secret by clicking the **Generate** button.
5. **Copy** and note down this secret, you will need it in GitHub and click the **create** button.
    <br>![](../ex1/images/create_credential.png)

6. Click **add** to add the repository.
    <br>![](../ex1/images/add_repo.png)

7. Click on the newly added repo and note down the `Payload URL` in **Webhook Event Receiver section**
    <br>![](../ex1/images/webhook_data.png)

8. In your project in GitHub, go to the **Settings** tab.

9. From the navigation pane, open **Webhooks**, then click on Add webhook.

10. Enter the Payload URL, Content type, and Secret from the Webhook Data pop-up in SAP Continuous Integration and Delivery. For all other settings, leave the default values.

11. Click on **Add webhook**.
<br>![](../ex1/images/add_webhook_github.png)

## Exercise 1.3 - Create a Pipeline Job

1. In SAP Continuous Integration and Delivery, go to the Jobs tab and click on + (Create job).
2. In the General Information section of the Create Job pane, enter the following values:

    - **Job Name**: Freely choose a unique name for your job. We recommend using a name that contains both your GitHub project name and branch e.g. `my-teched-job`
    - **Repository**: Select the repository you just created (if not already selected).
    - **Branch**: Enter `main`.
    - **Pipeline**: Keep the default `Cloud Foundry environment`.
  
    <br>![](/exercises/ex1/images/create_job.png)

3. In the Build section, Keep MTA as Build Tool and choose `Java 21 Node 22` as Build Tool Version.
    <br>![](/exercises/ex1/images/job_build_stage.png)

## Exercise 1.4 - Configure the Release Stage

To enable the **Release** stage in your SAP Continuous Integration and Delivery job, you need the name of the node for the upload to SAP Cloud Transport Management as well as a service key to authenticate your pipeline against it. We will provide these values to you.

1. In the **Release** stage in your job details, switch on **Cloud Transport Management** using the toggle.
2. Change the drop-down to `Export from` and enter `DEV` for the name of the initial transport node that we will create in Exercise 1.4 in SAP Cloud Transport Management Service.
3. To add a **Service Key**, click on the value help button. As a result, the **Select Credentials** window pops up. Then click the plus button which opens the **Create Credential** popup.
    <br>![](/exercises/ex1/images/job_release_stage.png)

4. In another browser window, open the SAP BTP cockpit and navigate to the **XP266_CENTRAL** subaccount in which the SAP Cloud Transport Management instance is available.
5. From the navigation area, choose **Services** → **Instances and Subscriptions**.
6. From the **Instances** area, find the **Service Key** named **XP266CTS** of Cloud Transport Management.
7. Here, in the **credentials** column click they *1 key* that has been created already and choose **Copy JSON** to copy the entire service key.
8. Back in SAP Continuous Integration and Delivery, paste the copied service key into the **Service Key** text box of the **Create Credentials** pop-up window.
    <br>![](/exercises/ex1/images/credential_add_ctms_key.png)

9. Enter a name for the service key, for example `ctms-servicekey`, then choose **Create**.

10. Click on **Create**. 

You've successfully created your first CI/CD job with the Build stage and release enabled. Changes committed to your GitHub repository will be automatically picked up by your delivery pipeline. However, before transport request is received by _SAP Cloud Transport Management service_, you need to create your transport landscape in the following exercise.

## Exercise 1.5 - Create Transport Landscape in SAP Cloud Transport Management Service

1. Open the UI of SAP Cloud Transport Management Service by entering the **XP266_CENTRAL** subaccount in which you have subscribed to the service and open the Instances and Subscriptions view.

2. In the Subscriptions area click on the **Cloud Transport Management** link.
    <br>![](/exercises/ex1/images/ctms_sub.png)

3. The overview page of **SAP Cloud Transport Management** where you navigate to **Landscape visualization**

4. You will now create a new transport landscape. This contains the creation of 3 transport nodes (DEV, QA and PRD) and 2 transport nodes.

5. Click the **+** sign to create your DEV node
   <br>![](/exercises/ex1/images/ctms_create_node.png)

   1. Enter as **Name** `DEV`.
   2. Optionally enter a **Description**, for example `Development node`.
   3. **Select** the **Allow Upload to Node** checkbox.
   4. Leave the **Forward Mode** set to `Pre-Import`.
   5.  As this is our initial entry note, select the **Virtual Node** checkbox.
   6.  Choose **OK**.
    <br>![](/exercises/ex1/images/ctms_dev_node.png)

6.  Click the **+** sign to create your QA node
    1. Enter as **Name** `QA`.
    2. Optionally enter a **Description**, for example `Testing node`.
    3. Do **not** select the **Controlled By SAP Solution Manager** & **Virtual Node** checkbox.
    4. Leave the **Forward Mode** set to `Pre-Import`.
    5. From the **Content Type** dropdown menu, select **Multi-Target Application**.
    6. Set the **Destination** to **Deploy_to_QA** pointing to your QA subaccount.
    7. Leave the **Deployment Strategy** set to **default**.
    8. Choose **OK**.
    <br>![](/exercises/ex1/images/ctms_qa_node.png)

7. Repeat this step for your PRD node. (Choose Destination **Deploy_to_PRD** in this case).

    `You should now see three transport nodes *DEV*, *TEST* and *PRD*.`

8.  Now create the **Transport Routes**. Click the connector button to create a new route.
   <br>![](/exercises/ex1/images/ctms_create_route.png)

9.  The first route connects the **DEV** **to** **QA** node. 
Enter the following for your first transport route and confirm the creation clicking **OK**:
   - Name: `DEV_to_QA`
   - Source Node: `DEV`
   - Target Node: `QA`
10. Repeat the same to connect your **QA** **to** **PRD** node. 
Enter the following second transport route and confirm the creation clikcing **OK**:
   - Name: `QA_to_PRD`
   - Source Node: `QA`
   - Target Node: `PRD`
  
Congratulations! You should now see the entire landscape transport in **Landscape visualization**.

## Summary

You've now set up SAP Continuous Integration and Delivery, added your GitHub repository to the service, configured a webhook, and created your first CI/CD job.

You also created your first transport landscape. At this point, you have everything setup to start a feature definition and development.

Continue to - [Maintain your Feature in Cloud ALM](../ex2/README.md)
