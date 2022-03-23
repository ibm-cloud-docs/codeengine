---
name: Translation ship NEXT
about: translation ship template
title: Translation ship NEXT
labels: translation-ship
assignees: ''

---



## Using this Issue for doc shipments to translation

This GitHub Issue contains the review checklist for what you need to do to send docs to translation for [Code Engine](https://cloud.ibm.com/docs/codeengine). 

## Review for the translation ship
As you go through the following list, mark off each item as you complete it.

### Prepare

- [ ] Know the date of the last ship to translation. **LAST_TRANSLATION_DATE**

- [ ] Know your charge-to ID. See the [Translation tools and access](https://test.cloud.ibm.com/docs/writing?topic=writing-translation-preparation) page for information about requesting a the charge-to ID for your project.
    - For Code Engine (2021): **BM160ABD289**

- [ ] Move this work item into the `In Progress` pipeline, make sure that the **translation-ship** label is added to the issue, and assign it to you.

- [ ] In the #doctopus-coligo](https://ibm-argonauts.slack.com/messages/CSYM4GUQ2) channel, check with the other writers and make sure that you're all clear to do a translation shipment. 

- [ ] Determine the word count delta from the previous translation shipment.  Use the [translation wordcounts tool](https://wcp-doctopus-docs-jenkins.swg-devops.com/).

- [ ] Review the Translation information on the [Translation Overview for {{site.data.keyword.cloud_notm}} Documentation](https://test.cloud.ibm.com/docs/writing?topic=writing-tp) page.  
    -  Use this page to determine your estimate for translation time for the package that you are preparing to send to translation. The estimate is based on your word count delta.

- [ ] Make sure you have the translation tools installed and ready to use.  See the [Translation tools and access](https://test.cloud.ibm.com/docs/writing?topic=writing-translation-preparation) page. 

- [ ] We are using TPT Light to send packages to translation. Make sure you have this tool and its prereqs installed and ready to use. See [Sending translation packages by using TPT Light](https://test.cloud.ibm.com/docs/writing?topic=writing-sending-translation-packages) page. 


### Prep the translation package

- [ ] Navigate to the current Code Engine published source in Git (`cloud-docs\codeengine` repo in the `publish` branch):
    * Code Engine docs: https://github.ibm.com/cloud-docs/codeengine/tree/publish

- [ ] Take a 2nd look and confirm you are working with the published source that you want to send to translation. 

- [ ] Download the source to your local machine. **TIP:** Download the zip such that you can easily find it in your `Downloads` directory. Uncompress the file on your local machine (remember where you put the files).

    **IMPORTANT:** If sending the translation package from a **Windows** machine, you must complete the following steps or the CHKPII checks will return the following error: `128 (W) UNIX file (newline=x'0A') should be converted to PC-DOS (newline=x'0D0A') format to be translated'.  To remove the error, complete following steps on **EACH** file:
    a. Open the file with Notepad++
    b. Click **Edit -> EOL Conversion -> Windows Format**
    c. Save the file

If sending the translation package from a **Mac machine**, you do not need to do the preceeding steps.


### Send the translation package

- [ ] See the [Sending translation packages by using TPT Light](https://test.cloud.ibm.com/docs/writing?topic=writing-sending-translation-packages) page for detailed instructions on using the tool.  
a. Open TPT Light and click **Create new package**.
b. Select the root directory where you have the files on your local machine that you want to send in the translation package. 
c. Select **Include subfolders**. 
d. Pick the files to include.  **Tip:** Click **Select all** and then remove the README.MD. You do not need to select images that don't require translation **WHAT ARE THESE??**
e. Click **Next**. This action runs CHKPII for you. 
f. Review the CHKPII results. Confirm that you have **0** errors.  
g. Enter the charge-to ID: For {{site.data.keyword.codeengineshort}} (2021): BM160ABD289
h. Provide a translation shipment name.
i. Complete the rest of the required fields and when ready click **Send**.


### After the translation package is sent

- [ ] In the summary of this issue, change `<next>` to the date the translation shipment was sent. 

- [ ] In this same repo, open a new issue by using the **Translation Ship** template. 
    - Set the **Pipeline** to `Backlog`, then click **New issue** and create a new issue.  
    - Set the label to `translation-ship`. 

- [ ] You will receive an email confirmation that the translation package was received and completed. 

- [ ] Update the new **Translation ship next** issue and add the date of this translation shipment (**LAST_TRANSLATION_DATE**) to the new issue.

- [ ] Close the current translation package issue. 

- [ ] Let writers know that the translation package was sent to translation.   

### When the shipment is returned 
**Shipment number** XXX
In this issue - check of the languages as they are returned
- [ ] de
- [ ] es
- [ ] fr
- [ ] ja
- [ ] ko
- [ ] pt_br

### When all language are returned 
- [ ] Run the [check-in tool](https://wcp-doctopus-docs-jenkins.swg-devops.com/job/translation-return-check-in/).
