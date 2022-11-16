---

copyright:
  years: 2022
lastupdated: "2022-11-16"

keywords: monitoring for code engine, performance metrics, monitor, metrics, requests, pods, application, attributes, jobrun, panic mode, custom dashboards

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


# Creating custom dashboards to monitor {{site.data.keyword.codeengineshort}} 
{: #monitor-custom}

Use {{site.data.keyword.mon_full_notm}} to gain visibility into the health and performance of {{site.data.keyword.codeengineshort}} workloads. You can customize a {{site.data.keyword.mon_short}} dashboard for {{site.data.keyword.codeengineshort}} workloads to a tailored set of metrics to help you identify bottlenecks or predict possible production problems.
{: shortdesc}


## Create custom dashboards to monitor {{site.data.keyword.codeengineshort}} 
{: #create-custom-monitor}

You can create a custom {{site.data.keyword.mon_short}} dashboard for {{site.data.keyword.codeengineshort}} workloads to a tailored set of metrics.
{: shortdesc}

Before you can create a custom dashboard in {{site.data.keyword.mon_short}}, you must first set up monitoring for {{site.data.keyword.codeengineshort}} workloads. Set up your {{site.data.keyword.mon_short}} service instance and enable Platform Metrics in the same region as the {{site.data.keyword.codeengineshort}} projects that you want to monitor. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region. For more information about setting up your {{site.data.keyword.mon_full_notm}} service instance and accessing your {{site.data.keyword.mon_full_notm}} metrics dashboard for monitoring {{site.data.keyword.codeengineshort}} workloads, see [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor). 

{{site.data.keyword.codeengineshort}} provides the `IBM {{site.data.keyword.codeengineshort}} Project Overview` dashboard, which is composed of pre-defined panels that monitor various aspects of {{site.data.keyword.codeengineshort}} workloads. You might want to create a custom {{site.data.keyword.mon_short}} dashboard for {{site.data.keyword.codeengineshort}} workloads to a tailored set of metrics.


1. Set up an [{{site.data.keyword.mon_full_notm}} service instance](/docs/codeengine?topic=codeengine-monitor#setup-monitor). To check for active {{site.data.keyword.mon_full_notm}} instances, see the [Observability dashboard](https://cloud.ibm.com/observe/monitoring). 

2. Ensure that there is monitoring data available. Because designing a custom dashboard is easier when you have data to monitor, it is important to have a running [application](/docs/codeengine?topic=codeengine-application-workloads) or [job](/docs/codeengine?topic=codeengine-job-plan). Some {{site.data.keyword.codeengineshort}} metrics exist only if they are available in the environment. 

3. Review the available [metrics](/docs/codeengine?topic=codeengine-monitor#metrics-by-plan) for {{site.data.keyword.codeengineshort}}.

4. Access your {{site.data.keyword.mon_full_notm}} metrics.
    1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
    2. Select **Monitoring**.
    3. Click **Open dashboard** to open the dashboard for your monitoring instance. 
    4. From the navigation menu, select **Dashboards->IBM->IBM {{site.data.keyword.codeengineshort}} Project Overview**. If you don't see the {{site.data.keyword.codeengineshort}} dashboard in the menu, you can start monitoring from your {{site.data.keyword.codeengineshort}} application or job by selecting **Launch Monitoring**.

5. Click **Create Custom Dashboard** to make a copy of the `IBM {{site.data.keyword.codeengineshort}} Project Overview` dashboard. Enter a name for your custom dashboard and click **Create and open**. For example, name your dashboard `My custom IBM Code Engine Project Overview`.

6. Customize your dashboard by adding or removing dashboard panels. For examples of how you might want to customize your dashboard for monitoring {{site.data.keyword.codeengineshort}} application and job run workloads, see [Scenario 1](/docs/codeengine?topic=codeengine-monitor-custom#custom-monitor-scenario1) and [Scenario 2](/docs/codeengine?topic=codeengine-monitor-custom#custom-monitor-scenario2). For more information about working with {{site.data.keyword.mon_full_notm}} dashboards, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards).

    Whenever you change the layout of your dashboard, be sure to click **Save Layout** to save your changes. You must save the layout changes or cancel before you continue to customize to your dashboard.
    {: tip}

7. Save the custom dashboard. The custom dashboard is available in the dashboard navigation menu, **Dashboards->My Dashboards**.

### Scenario 1: Focusing on {{site.data.keyword.codeengineshort}} application instances and job runs
{: #custom-monitor-scenario1}

Suppose you want to narrow the scope of monitoring {{site.data.keyword.codeengineshort}} workloads to focus on instances of your running applications and job runs. It can be useful to monitor this information because if your application scales to zero or your job or build isn't running, then you're not consuming resources. This scenario takes the `My custom IBM Code Engine Project Overview` dashboard that you previously created from the existing `IBM {{site.data.keyword.codeengineshort}} Project Overview` dashboard and simplifies the custom dashboard by modifying and removing panels.

1. Open your custom dashboard. This scenario assumes that you are starting with a copy of the `IBM {{site.data.keyword.codeengineshort}} Project Overview` dashboard. The custom dashboard is available in the dashboard navigation menu, **Dashboards->My Dashboards**.

2. Modify the `Total number of Applications` number panel and modify the query to display the actual number of instances by using the [`ibm_codeengine_application_actual_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_actual_instances) metric.

    1. Click the pencil icon to edit the panel. 
    2. From the Query tab, click the `ibm_codeengine_application_service_count` metric to modify the metric. Type `ibm_codeengine_` for a list of {{site.data.keyword.codeengineshort}} metrics. For this example, select the `ibm_codeengine_application_actual_instances` metric and specify a `Maximum` time aggregation and a `Maximum` group rollup. 
    3. From the Panel tab, rename this panel to `Total number of Application Instances`.  
    4. Click **Save** to save the changes for this panel.

3. Modify the `Total number of Application revisions` number panel and change the query to display the number of job runs by using the [`ibm_codeengine_jobruns`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_jobruns) metric. 

    1. Click the pencil icon to edit the panel. 
    2. From the Query tab, click the `ibm_codeengine_application_revision_count` metric to modify the metric. Type `ibm_codeengine_` for a list of {{site.data.keyword.codeengineshort}} metrics. For this example, select the `ibm_codeengine_jobruns` metric and specify a `Maximum` time aggregation and a `Maximum` group rollup. 
    3. From the Panel tab, rename this panel to `Total number of Job Runs`.  
    4. Click **Save** to save the changes for this panel.

4.  Delete the `Total number of Application routes` number panel by using the action menu.

5. Modify the `Applications overview` timechart panel and change the query to display monitoring information about your application and job run instances by using the [`ibm_codeengine_application_actual_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_actual_instances) and [`ibm_codeengine_jobruns`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_jobruns) metrics. 

    1. Click the pencil icon to edit the panel. 
    2. From the Query tab, keep the `ibm_codeengine_application_actual_instances` metric and remove the other rows of metrics by using the action menu for those metrics.
    3. From the Query tab, locate the `ibm_codeengine_application_actual_instances` metric and modify the segmentation to include application revision information. Click `ibm_codeengine_application_name` and add `ibm_codeengine_revision_name`. Make sure that you clear the selection for `Apply to All Queries`.
    4. From the Query tab, click **Add Query** to add a query for job runs. In the metric field, type `ibm_codeengine_` for a list of {{site.data.keyword.codeengineshort}} metrics. Select the `ibm_codeengine_jobruns` metric and specify a `Maximum` time aggregation and a `Maximum` group rollup. Specify the `ibm_codeengine_jobrun_condition` segmentation for this metric.
    5. Check that you only set the `ibm_codeengine_application_actual_instances` and `ibm_codeengine_jobruns` metrics for this panel. 
    6. From the Panel tab, change the name of this panel to `Application and Job Run Instances`.   
    7. Click **Save** to save the changes for this panel

6. Keep the panels that were updated in the previous steps for this scenario, but use the actions menu to delete other panels. After you remove panels that are not needed, you can adjust the size and layout of the individual panels to meet your needs. 

    Whenever you change the layout of your dashboard, be sure to click **Save Layout** to save your changes. You must save the layout changes or cancel before you continue to make changes to your dashboard.
    {: tip}

After you complete scenario 1, your custom dashboard includes three panels: `Total number of Application Instances`, `Total number of Job Runs`, and `Application and Job Run Instances`. 

### Scenario 2: Using PromQL queries with {{site.data.keyword.codeengineshort}} workloads
{: #custom-monitor-scenario2}

From the custom dashboard that you created in Scenario 1, suppose you want to use the Prometheus Query Language (PromQL) query feature of {{site.data.keyword.mon_full_notm}} to aggregate the number of applications and job runs metrics into one panel. In this scenario, let's use PromQL to add the number of application instances and the number of job runs into a single number panel. 

1. Open your custom dashboard that was customized with Scenario 1. The custom dashboard is available in the dashboard navigation menu, **Dashboards->My Dashboards**.  

2. Modify the `Total number of Applications` number panel and change the query to sum the number of application instances and the number of job runs.
    1. Click the pencil icon to edit the panel. 
    2. From the Query tab, click `PromQL` to use PromQL queries.
    3. From the Query tab, replace the contents of the query with `sum(max(ibm_codeengine_application_actual_instances) + max(ibm_codeengine_jobruns))`. Update **Options** to use `number` as the unit. Click **Run query**.
    4. From the Panel tab, rename this panel to `Total number of Application instances and Job Runs`.  
    5. Click **Save** to save the changes for this panel.
    
3. Use the actions menu to delete the `Total number of Job Runs` number panel because we aggregated both the total number of applications and job runs into a single number panel in the previous step. 

4. You can adjust the size and layout of the individual panels to meet your needs.   

    Whenever you change the layout of your dashboard, be sure to click **Save Layout** to save your changes. You must save the layout changes or cancel before you continue to customize to your dashboard.
    {: tip}

After you complete scenario 2, your custom dashboard includes two panels: `Total number of Application instances and Job Runs` and `Application and Job Run Instances`. 





