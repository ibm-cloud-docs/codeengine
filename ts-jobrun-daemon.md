---

copyright:
  years: 2020, 2023
lastupdated: "2023-08-10"

keywords: troubleshooting for code engine, troubleshooting jobs in code engine, troubleshooting daemon jobs in code engine, job run troubleshooting in code engine, job troubleshooting in code engine, daemon job, indefinitely

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my daemon job not automatically restart? 
{: #ts-jobrun-daemon}
{: troubleshoot}

I have a job that runs in `daemon` mode, which does not automatically restart after an error. 
{: tsSymptoms}

In {{site.data.keyword.codeengineshort}}, if you want your job to run indefinitely and not time out, you can specify to run the job in `daemon` mode. 
{: tsCauses}

If the container image for your code that is associated with your daemon job ends with a `0` exit code, {{site.data.keyword.codeengineshort}} assumes that the job was stopped intentionally, and the job is not restarted. 

{{site.data.keyword.codeengineshort}} automatically restarts a job that runs indefinitely if the code for the container image that is associated with the daemon job exits with a nonzero exit code. So, if the daemon job fails for an unexpected reason, such as an out of memory condition, then {{site.data.keyword.codeengineshort}} automatically restarts the daemon job when the code ends with a nonzero exit code.
{: tsResolve} 

For more information, see [Creating and running a job that runs indefinitely](/docs/codeengine?topic=codeengine-job-daemon)





