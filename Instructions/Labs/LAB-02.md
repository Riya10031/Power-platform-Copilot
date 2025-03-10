# Module 2: Create an approval flow with Copilot in Power Automate

## Lab Scenario

In this exercise, you will create an approval flow using Power Automate. Your objective is to automate a process where a request is submitted and requires approval before proceeding. Start by accessing Power Automate and selecting the option to create a new flow. Use the built-in templates or create a flow from scratch, setting up triggers and actions to handle the approval process. Configure the flow to send approval requests to designated users, capture their responses, and perform actions based on their decisions. This exercise will demonstrate how to automate and streamline approval workflows efficiently.

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1 : Create an approval flow.
- Task 2 : Update the flow ,send an email and Run the App.
  
## Task – 01: Create an approval flow.

In this task, you'll create an approval flow using Power Automate to automate the process of submitting requests for approval. You'll configure the flow to handle approval requests, capture responses, and execute actions based on those responses.

1. Open a new tab and browse to [https://make.powerautomate.com](https://make.powerautomate.com). From the top menu, select the **Copilot** environment that you created in the previous task.

    ![screenshot of the prompt ](../Media/powerautomate-1.png)

1. In the center of the Home page within Power Automate enter the following prompt: ` Request approval when a dataverse record with a approvals and condition below approvals true or false `, Select the **Generate** button .

   ![screenshot of the prompt ](../Media/dataverse-10.png)

1. On the **Describe it to design it** prompt, Copilot provides the outline for a suggested flow that you can review. To accept the flow, select **Keep it and continue**

    ![screenshot of the prompt ](../Media/keepitcontinue-1.png)
   
1. Review the connected apps and services. If a connection hasn't been made, edit or fix it and then select **Create flow**.The Edit with Copilot designer opens with your flow along with a Copilot chat window on the right.
  
1. Set up some parameters by selecting the **When a row is added,** modified or deleted trigger. A panel on the left side of the screen shows the trigger details, including an empty Table Name parameter that's required.

1. From the **Change type** dropdown menu select **Added (1)**. From the Table Name dropdown menu, search for and select **Real Estate Showings (2)**.

   ![screenshot of the prompt ](../Media/whenarowmodified.png)

1. Select the **Start and wait for an approval action**. Notice that the Approval Type parameter is missing.

   ![screenshot of the prompt ](../Media/02/power-automate-copilot-approval-type.png)

1. From the **Approval Type dropdown** menu, select **Approve/Reject - First to respond**.After you select the Approval Type, more parameters are now available.

   ![screenshot of the prompt ](../Media/02/power-automate-copilot-approval-type-selected.png)

1. In the Copilot chat window, enter the following prompt:  Add "**New Request for Real Estate Showing**" as the Title parameter for the **Start and wait for an approval action** ,It takes a few seconds for Copilot to process the prompt. When processing is complete, the Title parameter is populated with the prompt text.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-title-parameter.png)

1. For the Assigned To parameter, enter and select **<inject key="AzureAdUserEmail"></inject>** that you're using for this lab. This email address is the one that receives the approval request.

1. For the Details parameter, enter the following text:
    
    ```
    A new request for a real estate showing has been created. Please review the details below and approve or reject the request:
    Property:
    Client:
    Client Email:
    Date:
    Time:
    ```
      ![screenshot of the prompt ](../Media/02/power-automate-copilot-details-parameter.png)

1. Place your curser next to Property: in the Details parameter and then select the lightning icon to open the Dynamic content pane.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-dynamic-content-icon.png)

1. In the Dynamic content pane, select See More to expand the list of available dynamic content.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-see-more.png)

1. Scroll down until you find the **Address** field and then select it.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-property-field.png)

1. The  **Address** dynamic content field is now added to the Details parameter.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-property-field-added.png)

1. Complete the same steps for the **Address, Client (Client Full name) , Name, Client Email , Date, and Time fields**, When you're done with the rest of the fields, the values should resemble the following image.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-details-parameter-added(1).png)

1. With the Details parameter completed, you can collapse the **Start and wait for an approval action** by selecting the double arrow icon.

    ![screenshot of the prompt ](../Media/copilot-start-wait-approval-collapsed-1.png)

1. Select the **Condition** action. select **Outcome** from the Dynamic content pane.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-outcome.png)

1. Select **is equal to** and then enter **Approve**.

1. Collapse the **Condition** action and then select the **Update a row** action under the **True** branch of the condition.

    ![screenshot of the prompt ](../Media/condition-01-02.png)

1. From the Table Name dropdown menu, search for and select **Real Estate Showings**.

1. Select the **Row ID field** and then select the **Real Estate Showings** unique identifier field from the Dynamic content pane.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-row-id.png)

1. Select Show all under **Advanced parameters**.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-show-all.png)

1. Select **Completed** from the **Status** dropdown menu.

    ![screenshot of the prompt ](../Media/status-completed-01.png)

    >**Note:** When a showing is approved, the Status field in the Real Estate Showings table is updated to Completed.

1. Collapse the **Update a row** action and then select the **Update a row 2** action under the **False branch** of the condition.

1. From the Table Name dropdown menu, search for and select **Real Estate Showings**, select the **Row ID** field and then select the **Real Estate Showings** unique identifier field from the Dynamic content pane.

    ![screenshot of the prompt ](../Media/updaterow2sel.png)

1. Select **Show all** under **Advanced parameters**.

1. Select **Cancelled** from the Status dropdown menu.When a showing is rejected, the Status field in the Real Estate Showings table is updated to Cancelled.

    ![screenshot of the prompt ](../Media/cancelled.png)

1. Collapse the **Update a row 2** action.

## Task-02: Update the flow ,send an email and Run the App.

In this task, you'll update the approval flow to refine its settings and configure it to send an email notification. After making these updates, you'll run the app to test and ensure the flow and email notifications work correctly.

1. In the Copilot chat window, enter the following prompt and submit it: Under the "**Update a row**" action for both branches in the condition, add a new **"Send an email"** action. After a few seconds, Copilot should explain what it did, as shown in the following image.

   ![screenshot of the prompt ](../Media/sendanemailaction.png)

1. Select the **Send an email** action under the **True branch** of the condition.

1. In the **To** field, select **Client Email** from the Dynamic Content pane under **Where a row is added, modified, or deleted**.

    >**Note:** If you are unable to see the dynamic content pane, select **Switch to Advanced mode**, which is above the **To** field.

1. For the Subject field, enter the following text: Add `Your request for a real estate showing has been approved` as the Subject parameter for the Send an email action

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-subject-parameter.png)

1. For the Body field, enter the following text: Add **Good day - Your request for a real estate showing has been approved. Please see below for details.** as the Body parameter for the Send an email action. The Body field should populate with the prompt text.

   ![screenshot of the prompt ](../Media/02/power-automate-copilot-body-parameter.png)

1. Enter the following content after the Body text:

    ```
    Property:

    Client :

    Client Email:

    Date:

    Time:
   ```

    >**Note** : Add the **Address, Client Full name , Client Email,  Date, and Time** fields from the Dynamic content pane to the appropriate lines in the Body text.

    ![screenshot of the prompt ](../Media/body-01.png)

1. Add the **Response summary field** from the Dynamic content pane to the end of the Body text.

   ![screenshot of the prompt ](../Media/response-summary.png)

1. Collapse the **Send an email** action.

1. Select the **Send an email 2** action under the **False branch** of the condition.

1. In the **To** field, select **Client Email** from the Dynamic Content pane under **Where a row is added, modified, or deleted**.

    >**Note:** If you are unable to see the dynamic content pane, select **Switch to Advanced mode**, which is above the **To** field.

1. For the Subject field, enter the following text: Add `Your request for a real estate showing has been rejected` as the Subject parameter for the Send an email action.

1. For the Body field, enter the following text: Add `Good day - Your request for a real estate showing has been rejected. Please see below for details.` as the Body parameter for the Send an email action.

1. Enter the following content after the Body text:

    ```
    Property:

    Client :

    Client Email:

    Date:

    Time:
    ```
    >**Note**: **Add the Address, Agent Name, Date, and Time fields from the Dynamic content pane** to the appropriate lines in the Body text.

1. Add the **Response summary field** from the Dynamic content pane to the end of the Body text, Collapse the Send an email action.

    ![screenshot of the prompt ](../Media/bodyemailaddress.png)

1. Rename the flow to **Request Approval for Real Estate Showing** by selecting the request approval when a Dataverse record is created text in the upper-left corner of the screen.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-rename-flow.png)

1. **Save** the flow by selecting the Save button in the upper-right corner of the screen.

    ![](../Media/02/power-automate-copilot-save.png)

1. Test the flow by selecting the Test button in the upper-right corner of the screen. Select **Manually** and then select **Test**.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-test.png)

1. To submit a **real estate showing request**, go to the Real Estate Showings app in Power Apps.

1. Run the app and then select **+New to create** a new showing request.Fill in the fields with the following information:

    - Agent Name - < random name >
    - Client Full Name - < Your name >
    - Client Email - < Your email > (the email that you're using for this lab)
    - Date - < Any future date >
    - Time - < Any future time >
    - Status - Pending
    - Address - 210 Pine Road, Portland, OR 97204
    
    >**Note:** This address is one of the addresses from the Microsoft Excel file in Module 1; it's the same file that you uploaded and turned into the Real Estate Properties table. Usually, you would have a lookup field to the Real Estate Properties table, but not for this lab to keep it simple.Select the check mark in the upper-right corner of the screen.

1. Select the X in the upper-right corner to close out of the app.The flow runs and sends an approval email to the email address that you provided in the flow that you built.
Sign in to the email account that you're using for this lab and then wait for the email to arrive.

    >**Note**: If the flow doesn't run immediately, make sure that you wait for it. It might take up to 10 minutes for the flow to be triggered, especially on the first try.

    - The approval should resemble the following image.

        ![screenshot of the prompt ](../Media/02/power-automate-copilot-approval-email.png)

1. Select **Approve**. Add a comment and then select **Submit**.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-approval-submitted.png)

1. The flow continues to **run**; it updates the row and sends an email to the requestor. The email that's sent to the requester resembles the following image.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-approval-emails.png)

1. Check the flow and notice that the flow is now marked as **Succeeded** in the **run history**.

    ![screenshot of the prompt ](../Media/02/power-automate-copilot-flow-succeeded-1.png)

## Summary

In this lab, you have accomplished the following:

- You have created an approval flow and updated it to send an email notification.

- You have run the app to verify that the approval process and email notifications work correctly.
