---
title: Create a batch job
description: A batch job is a group of tasks that are submitted to an Application Object Server (AOS) instance for automatic processing.
author: matapg007
ms.date: 03/18/2024
ms.topic: how-to
ms.custom: 
  - bap-template
audience: Application User
ms.reviewer: johnmichalak
ms.search.region: Global
ms.author: matgupta
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: Version 7.0.0
ms.search.form: BatchJob, SysRecurrence, BatchAlerts
---
# Create a batch job

[!include [banner](../../../finance/includes/banner.md)]

A batch job is a group of tasks that are submitted to an Application Object Server (AOS) instance for automatic processing. Batch jobs are run by using the security credentials of the user who created the job. Use the following procedure to create a batch job. The demo data company used to create this procedure is USMF.

## Create the batch job

1. Go to **System administration \> Inquiries \> Batch jobs**.
2. Select **New**.
3. In the **Job description** field, enter a description of the batch job.
4. In the **Scheduled start date/time** field, enter the date and time when the batch job should run.
5. Select **Save**.

## Create a recurrence

1. On the Action Pane, select **Batch job**.
2. Select **Recurrence**. Use these options to enter a range and pattern for the recurrence.
3. Select **OK**.

> [!NOTE]
> All recurring batch jobs are automatically returned to the waiting state, regardless of whether they fail or succeed. This behavior ensures that recurring jobs can complete any pending work during the next run if the previous run failed. This functionality can be enabled only if the batch job's recurrence conditions are still valid. For example, the batch job must have a remaining recurrence count or a recurrence end date that hasn't passed.

## Add alerts

1. On the Action Pane, select **Batch job**.
2. Select **Alerts**. Indicate if you want alert messages sent when the batch job ends, has an error, or is canceled. Then specify if you want the alerts to be displayed as pop-up messages.
3. Select **OK**.

## Add a task to a batch job

1. On the **Batch jobs** page, select **View tasks**.
2. Select **Ctrl+N** to create a task.
3. Enter a description of the batch task.
4. In the **Company accounts** field, select the company database that the task should run in.
5. In the **Class name** field, select the process that the task should run. 
6. As appropriate, select a batch group for the task.

    Client tasks must be assigned to a batch group. They're automatically assigned to the default batch group (also known as the Empty batch group).

7. Select **Ctrl+S** to save the task.
8. To make the selected task dependent on another task in the job, select the **Has conditions** grid, and then follow these steps for each condition that you want to define:

    1. Select **Ctrl+N** to create a condition.
    2. Select the task ID of the parent task.
    3. Select the status that the parent task must reach before the dependent task can run.
    4. Select **Ctrl+S** to save the condition.

    If you define more than one condition, and if *all* the conditions must be met before the dependent task can run, select a condition type of **All**. If the dependent task can run after *any* of the conditions is met, select a condition type of **Any**.

9. Select how task failures should be handled. To ignore the failure of a specific task, on the **General** tab, select the **Ignore task failure** option for that task. If this option is selected, failure of the task doesn't cause the job to fail. You can also use the **Maximum retries** field to specify the number of times that a task should be retried before it's considered to have failed. As a best practice, we recommend that you not set the **Maximum retries** field to a value that is more than **5**.

    For more information about batch retries, see [Enable batch retries](../../dev-itpro/sysadmin/retryable-batch.md).

## Batch job history

1. Under the **Batch Jobs** in **Save Jobs to History**, you can select one of three options: **Always**, **Errors Only**, or **Never**.

    - **Always** – The history for the job is always created, irrespective of terminal status of the batch job.
    - **Errors Only** – The history of the job is only created if the job ended in the error state.
    - **Never** – No history is created for the batch job.

3. If the batch job has many batch tasks, we recommend that you set this field to **Errors Only** or **Never**.

> [!IMPORTANT]
> Starting with release 10.0.39, If the batch job has more than 5,000 batch tasks, then the corresponding job history would only save first 2,500 tasks, preferring tasks with status in following order: **Error** \> **Cancelled** \> **Finished** \> **Not Run**. This measure has been implemented to prevent blocking batch-related tables that might occur due to such large jobs.

## Adjust batch job status

1. Go to **System administration** \> **Inquiries** \> **Batch jobs**.
2. Select the appropriate batch job.
3. On the Action Pane, select **Batch job** \> **Functions** \> **Change status**.
4. Select the appropriate status:

    - **Withhold** – Set the batch job as **withhold** so it's withheld from the batch job scheduler. Equivalent to *stop*.
    - **Waiting** – Set the batch job as **waiting** so it's waiting to be picked up by the batch job scheduler. Equivalent to *go*.

5. Select **OK**.

[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
