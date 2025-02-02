---
title: "6 - Share events for discovery by others"
description: "Publish the results of your event processing to the Catalog to allow them to be shared and reused by others."
permalink: /tutorials/guided/tutorial-6
toc: true
section: "Guided tutorials for IBM Event Automation"
cardType: "large"
order: 6
---

{% include video.html videoSource="videos/tutorials/guided/06-discover.mp4" %}{: class="tutorial-video" }

## Scenario: Sharing results of analysis and processing
{: #scenario}

The EMEA operations team wants to share their new topic of EMEA orders for use by other teams in their enterprise.

## Instructions

### Step 1 : Create a flow

This tutorial begins with the flow that is created in [Triggering actions](./tutorial-5).

If you haven't completed that tutorial yet, you should do it now.

### Step 2 : Add the topic to the catalog

The next step is to provide the topic details to create an entry in the catalog.

1. Go to the **{{site.data.reuse.eem_name}}** topics page.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-1.png "screenshot of the EEM topics page"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-1.png "screenshot of the EEM topics page")

   If you need a reminder of how to access {{site.data.reuse.eem_name}}, you can review [Accessing the tutorial environment](./tutorial-access#event-endpoint-management).

1. Click the **Add topic** button.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-2.png "screenshot of the EEM topics page"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-2.png "screenshot of the EEM topics page")

1. Reuse the existing connection details of the {{site.data.reuse.es_name}} cluster.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-3.png "screenshot of the EEM topics page"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-3.png "screenshot of the EEM topics page")

1. Choose the new `ORDERS.EMEA` topic created in [the previous tutorial](./tutorial-5).

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-4.png "screenshot of EEM"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-4.png "screenshot of EEM")

1. Click **Add topic**.

### Step 3 : Document the topic

The next step is to document the topic to describe the events that your processing flow is producing.

1. Click the new `ORDERS.EMEA` topic.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-5.png "screenshot of EEM"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-5.png "screenshot of EEM")

1. Use **Edit information** to provide documentation for the topic.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-6.png "screenshot of EEM"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-6.png "screenshot of EEM")

1. Add a description of the events generated by your processing flow.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-7.png "screenshot of EEM"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-7.png "screenshot of EEM")

   Suggested description:
   > "Events from the EMEA region recorded by the order management system"

1. Use the Copy button in {{site.data.reuse.es_name}} to get a recent example message from the topic.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-8.png "screenshot of Event Streams message viewer"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-8.png "screenshot of Event Streams message viewer")

1. Add the sample message to the documentation for the topic.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-9.png "screenshot of catalog edit form"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-9.png "screenshot of catalog edit form")

1. Click **Save**.

### Step 4 : Publish the topic

The final step is to publish the new topic in the catalog so that it can be discovered by other teams in your enterprise.

1. Click the **Publish topic** button in the **Manage** tab.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-10.png "screenshot of topics editor"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-10.png "screenshot of topics editor")

1. Choose the default gateway group.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-11.png "screenshot of topics editor"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-11.png "screenshot of topics editor")

1. Confirm that the topic is published by switching to the catalog.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-12.png "screenshot of catalog"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-12.png "screenshot of catalog")

1. Confirm that your sample message and description are displayed in the topic details page.

   [![screenshot]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-13.png "screenshot of catalog"){: class="tutorial-screenshot" }]({{ 'images' | relative_url }}/ea-tutorials/tutorial-6-13.png "screenshot of catalog")

## Recap

You published the results of your event processing flow to a catalog.

The documentation you provided will enable other people in your enterprise to make use of the events your flow is producing, and the catalog will allow them to create their own credentials for using the topic.

## Next step

You have completed the guided tutorial. You used all three capabilities in {{ site.data.reuse.ea_long }}: creating topics in {{site.data.reuse.es_name}}, discovering and publishing topics in {{site.data.reuse.eem_name}}, and processing events in {{site.data.reuse.ep_name}}.

If you would like more ideas of things to try in {{site.data.reuse.ep_name}}, we have more [Tutorials for Event Processing]({{ 'tutorials/event-processing-examples/example-03' | relative_url }}), which are there to show you other things that you can do, and inspire you with ideas for your own projects.
