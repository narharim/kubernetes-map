___
- Some tasks are short-lived and only need to run once and then finish. 
- Examples include:    
	- Generating thumbnail from image	    
	- Running data analytics	    
	- Generating a report and sending an email
- These are called **batch workloads**.

___
## Jobs using Pod
- You create a [[Pod]] that performs the math operation.
- The pod starts, does the job, and exits but Kubernetes tries to restart the pod again and again. Why?  
- Because of the `restartPolicy`, which is set to `Always` by default. 

___
## Stop from restarting It
- To prevent restart:
     - Set the pod’s `restartPolicy` to `Never` or `OnFailure`
	- Now the pod runs once and doesn’t restart after completion.
- But we still have a problem...

## Multiple Pods for a Job
- Sometimes your task is large and needs to be ran across multiple pods.
 - You want to run multiple pods and make sure all of them finish successfully,
- ReplicaSets won't help here because they are meant to keep number of pods running all the time
___
## That’s Where Jobs Come In
- A Job creates one or more pods and makes sure they finish the task
    
___
##  How to Create a Job

```yaml
	apiVersion: batch/v1
	kind: Job
	metadata:
	  name: download-job
	spec:
	  template:
	    spec:
	      restartPolicy: Never
	      containers:
	        - name: downloader
	          image: curlimages/curl
	          command: ["curl", "-O", "https://example.com/data.csv"]
```

___
###  Running Multiple Pods
- To run more than one pod, set the `completions` field.  
- For example:
    ```Yaml
    completions: 3
    ```
- This will run 3 pods, one after another.

___
### What If Some Pods Fail?

- Kubernetes will keep creating new pods until it gets the desired number of successful completions.
- For example:
    - You ask for 3 completions.        
    - If 2 pods succeed and 1 fails, Kubernetes tries again until 3 succeed total.
___
### Running Pods in Parallel
- By default, job runs pods sequentially.
- To run them at the same time, add the `parallelism` field.
- For Example:

	```yaml
	parallelism: 3
	completions: 3
    ```

This means:
- Run 3 pods at once and If only 2 succeed, it creates 1 more pod and keeps doing this until 3 pods succeed


___
## Commands
1. Create a job
> `kubectl create -f job.yaml`
2. Check job status
> `kubectl get jobs`
3. Get logs for job    
> `kubectl logs <pod-name>`
4. To delete the job
> `kubectl delete job <job-name>`

___
⬅️ [[]] | [[Cron Job]] ➡️
### References
1. https://kubernetes.io/docs/concepts/workloads/controllers/job/