___
- you can create [[Jobs]] to run number of task inside [[Pod]]
- It run instantly and completes
___
## Run Periodically or At Schedule Time


```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox:1.28
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure

```
- The `.spec.schedule` field is required. The value of that field follows the [Cron](https://en.wikipedia.org/wiki/Cron) syntax
- The `.spec.jobTemplate` defines a template for the Job that CronJob creates.
- The `.spec.jobTemplate.spec.template` defines a template for actual Job

## Commands
1. Create a cronjob
> `kubectl create -f cronjob.yaml`
2. Check cronjob detail
> `kubectl get cronjob`
3. To delete the cronjob
> `kubectl delete cronjob <job-name>`


___
⬅️ [[]] | [[]] ➡️
### References
1. https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/