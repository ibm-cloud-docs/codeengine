---

copyright:
  years: 2020, 2023
lastupdated: "2023-08-14"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, parallel jobs, parallel batch jobs
subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Running jobs in parallel
{: #job-run-parallel}

Learn how to run jobs in {{site.data.keyword.codeenginefull}} with operational efficiencies. 
{: shortdesc}

## How can I efficiently process a large number of files by using job processing?
{: #job-run-parallel-how}

Suppose that you have many files that are stored in an {{site.data.keyword.cos_full_notm}} bucket and you want to use batch processing in {{site.data.keyword.codeengineshort}}. The objective is to read files from one bucket, manipulate the files and store the files in a different {{site.data.keyword.cos_short}} bucket in the most efficient way. Let's assume you have 2000 files in the input bucket each day.  All the files have different file name and the file names begin with an alphabetic character (A-Z, a-z). 

As you plan a solution for this scenario, you first think about an event-based solution. In this case, for every file that is written to the input {{site.data.keyword.cos_short}} bucket, an event is created and a {{site.data.keyword.codeengineshort}} application is called. Using events, a single file might trigger individual processing, which can be inefficient for many files. 

Can running a batch job be a better approach? Yes it can! Let's see why batch jobs are better suited for handling multiple files together.

1. Determine an approach to divide the set of files into parallel streams. Let's divide the files based on the first character of the file name. With this approach, you can have 26 streams, with each stream responsible for files that begins with one specific character. You can identify a specific stream by reading the automatically injected `JOB_INDEX` environment variable of a running job instance. See [Automatically injected environment variables for jobs](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-jobs). For this example, you can configure your job instances by either specifying the number of instances as `26` or the array indices as `0-25`. 

    Each running job instance is assigned an index from 0 to 25. In your code, use the following pattern to distribute the input data to the job instances. 
    * job instance with JOB_INDEX=0 works on files that start with `A` or `a`  
    * job instance with JOB_INDEX=1 works on files that start with `B` or `b`
    * job instance with JOB_INDEX=2 works on files that start with `C` or `c`   
    * [D ... y]
    * job instance with JOB_INDEX=25 works on files that start with `Z` or `z`

    Because each stream is processing multiple files, define the queue length of a stream as the number of files that are processed by the single stream.

2. In {{site.data.keyword.codeengineshort}}, [create the job and its configuration](/docs/codeengine?topic=codeengine-job-plan). 
    * Specify the job array indexes as `0-25`, which represents the 26 parallel streams. 
    * Specify the CPU and memory resources for your job, or take the defaults. Each job index gets the same CPU and memory resources that you specify for the job; for example, 1 vCPU and 4 GB memory. 


3. [Run your job](/docs/codeengine?topic=codeengine-run-job). In the {{site.data.keyword.codeengineshort}} console, you can view the number of job indexes that are pending, running, and completed. The job ends when the last job index completes its run. 


## Benefits of running parallel batch jobs 
{: #job-run-parallel-benefit}

This approach of implementing parallel batch jobs offers benefits. 

* Reduced initialization -  Because one job index processes files with similar starting characters, only one initialization or connection setup is required per job index. This approach saves resources and costs when compared to individually initializing on a per file basis. With the parallel job solution, there are 26 initializations instead of 2000 initializations. 

* Efficient resource usage - By dividing the task into parallel longer running streams, this solution uses available resources more efficiently, while processing speed is maximized. 

## Considerations when planning parallel batch jobs 
{: #job-run-parallel-consider}

Consider the following points when you plan parallel batch job solutions. 

* Balancing parallel job indexes and queue length -  It's essential to find a good balance between the number of streams (parallel job indexes) and the queue length. Too few job indexes cannot fully use available resources, while too many indexes can increase the initialization processing and increase the load on cloud services, such as {{site.data.keyword.cos_short}}. This effect can result in rate limits when calling other cloud services.

* Similar job processing time -  When you plan your solution, consider that each job index takes about the same time to complete its task. Avoid scenarios where one job index takes significantly longer than others, as the processing time might cause inefficiencies in resource usage and increase the job processing time.

* Use of multiple jobs - For the previous scenario, another variation of the solution uses multiple jobs. Consider creating 2 batch jobs, one for files that start with `A - Z` and another for files that start with `a - z`. Without any changes to code, you can trigger these jobs either in parallel or sequentially, based on your processing requirements and resource availability. 

* Use of multiple jobs - For the previous scenario, a different approach is to use multiple jobs. These multiple jobs do not rely on the configured array indices. Instead, consider creating 2 batch jobs, one for files that start with `A - Z` and another for files that start with `a - z`. Without any changes to your code, you can trigger these 2 jobs either in parallel or sequentially, based on your processing requirements and resource availability.

*  Job triggering mechanism - You can choose to trigger the job with a [cron subscription](/docs/codeengine?topic=codeengine-subscribe-cron) at specific intervals, or with a trigger application that monitors the {{site.data.keyword.cos_short}} bucket for new files and initiates the batch processing as needed. Depending on your scenario, you can optimize {{site.data.keyword.codeengineshort}} use for cost efficiency versus response time for how quickly the files are processed after they are written to the bucket.




