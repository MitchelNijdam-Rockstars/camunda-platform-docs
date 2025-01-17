---
id: implementing-connectors
title: Implement connectors
description: "Connectors communicate with any system or technology, reducing the time it takes to automate and orchestrate business processes across systems."
keywords: [connector, modeling, connectors, low-code, no-code]
---

The launch of [Camunda Platform 8](../components/concepts/what-is-camunda-platform-8.md) also introduced an integration framework with a key goal: integrate faster to reduce the time it takes to automate and orchestrate business processes across systems.

[Connectors](../components/modeler/web-modeler/connectors/index.md) achieve this goal. Ready to use out of the box, connectors help automate complex [business processes](../components/concepts/processes.md) by inserting them into [BPMN diagrams](./automating-a-process-using-bpmn.md) within [Web Modeler](../components/modeler/about.md), and configuring them via the properties panel.

Connectors technically consist of two parts: the business logic is implemented as a [job worker](../components/concepts/job-workers.md), and the user interface during modeling is provided using an element template. In this guide, we'll walk step-by-step through the implementation of a sample connector.

## Set up

We'll implement our connector with [Modeler](../components/modeler/about.md). To get started, ensure you’ve [created a Camunda Platform 8 account](./guides/create-account.md).

You'll also need to [create a SendGrid account](https://signup.sendgrid.com/) if you don't have one already, as we'll use SendGrid in our example connector. Once you've created your account, you will immediately be prompted to create a [sender](https://docs.sendgrid.com/ui/sending-email/senders).

### Create a cluster

import CreateCluster from './assets/react-components/create-cluster.md'

<CreateCluster/>

## Getting started

Once logged in to your Camunda Platform 8 account, take the following steps:

1. Click on the **Modeler** tab at the top of the page, and click **New project**.
2. Name your project. In this example, we'll name ours `Expense process`.
3. Select **New > BPMN Diagram > + Create blank**.
4. Give your model a descriptive name, and then give your model a descriptive id within the **General** tab inside the properties panel on the right side of the screen. In this case, we've named our model `Submit expense` with an id of `submitting-expense`.

## Build a BPMN diagram

Use Web Modeler to design a BPMN flow with the appropriate tasks. To get started, create a task by dragging the rectangular task icon from the palette, or click the existing start event and the displayed task icon.

In this example, we've designed the following BPMN diagram:

![bpmn example diagram](./img/bpmn-expense-sample.png)

:::note
To learn more about building your own BPMN diagram from scratch, visit our guide on [automating a process using BPMN](./automating-a-process-using-bpmn.md).
:::

## Add a connector

Here, a receipt is initially uploaded for review. The first task we need to complete is notifying the manager of the uploaded receipt. If we want to leverage our email service to notify the manager, we can utilize a productivity applications connector to replace this task.

:::note
Camunda offers a variety of available connectors. For example, utilize cloud connectors to communicate with cloud-native applications and conform to REST, GraphQL, or SOAP protocols. Or, employ service connectors to integrate with technology enablers like RPA, AI or IOT services. Learn more about our [available connectors](../components/modeler/web-modeler/connectors/available-connectors/index.md) to find out which may best suit your business needs.
:::

To add our productivity applications connector, take the following steps:

1. Click the start event. A context pad to the right of the start event will appear.
2. Click the **Append connector** item in the panel.
3. To send an email via SendGrid, for example, select the **SendGrid Email Connector** option. Name this newly-created task `Notify manger of receipt`. This now replaces our original task.
   ![adding a connector](./img/adding-connector.png)
4. You need to fill out the required information in the properties panel of this task on the right side of the screen. Here, we'll add an example API key obtained from our [SendGrid account](https://app.sendgrid.com/settings/api_keys), a sender and receiver name and email address, and the email message content.

![filling out connector properties panel](./img/connector-properties-panel.png)

Our connector is now attached and ready to use. Your completed diagram should look like the following:

![completed connectors and BPMN diagram](./img/connectors-bpmn-diagram.png)

## Execute your process diagram

:::note
If you change a diagram and it is autosaved, this has no effect on your cluster(s).

When you deploy the diagram, it becomes available on the selected cluster and new instances can start.
:::

To execute your completed process diagram, click **Deploy diagram**.

You can now start a new process instance to initiate your process diagram. Click **Start instance**.

You can now monitor your instances in [Operate](./components/operate/index.md). From your diagram, click the honeycomb icon button next to the **Start instance** button, and **View process instances**. This will automatically take you to Operate to monitor your running instances.

:::note
Variables are part of a process instance and represent the data of the instance. To learn more about these values, variable scope, and input/output mappings, visit our documentation on [variables](../components/concepts/variables.md).
:::

## Observe your running process

After the [user task](./getting-started-orchestrate-human-tasks.md) **Upload receipt** is completed in [Tasklist](../components/tasklist/introduction.md), an email is automatically sent to the address as specified in the connectors properties panel we configured earlier.

![email via SendGrid](./img/sendgrid-email.png)

In [Operate](../components/operate/index.md), you will now see the process move forward to **Review receipt**.

![operate example](./img/operate-example.png)

## Additional resources and next steps

- [Connectors documentation](../components/modeler/web-modeler/connectors/index.md)
- [Available connectors](../components/modeler/web-modeler/connectors/available-connectors/index.md)
- [Connectors & Integration Framework](https://camunda.com/platform/modeler/connectors/)
- [Camunda BPMN Tutorial](https://camunda.com/bpmn/)
- [Automate processes using BPMN](./automating-a-process-using-bpmn.md)
