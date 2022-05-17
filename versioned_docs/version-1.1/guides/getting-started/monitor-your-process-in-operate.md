---
id: monitor-your-process-in-operate
title: Monitor your process in Operate
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Camunda Cloud offers Operate to monitor your process instances.

:::note
Find an entry point in the cluster details.
:::

![operate-dashboard](./img/operate-dashboard.png)

By selecting the deployed process, you will see a list of instances that can be filtered:

![operate-instances](./img/operate-advanced-instances-pong.png)

Because [the started worker](./implement-service-task.md) returns the following, the process ends in the upper end event following the Ping sequence flow:

```json
{
  "return": "Pong"
}
```

Changing the worker to the following and creating a new instance leads to a second instance in Operate:

```bash
zbctl create worker test-worker --handler "echo {\"return\":\"...\"}"
```

You'll see this ending in the second end event following the else sequence flow:

![operate-instance](./img/operate-advanced-instances-other.png)

As a next step, you can now connect both workers in parallel and create more process instances:

```bash
while true; do zbctl create instance camunda-cloud-quick-start-advanced; sleep 1; done
```

In Operate, you'll see instances ending in both end events depending on which worker picked up the job.

![operate-instances](./img/operate-advanced-instances.png)