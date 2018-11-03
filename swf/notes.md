# Simple Web Flow

Simple Web Flow (SWF) consists of the following `Actors`

- `Workflow Starters` - these are applications that can start a workflow. You can think of this as the application which invokes or calls the SWF pipeline steps.
- `Deciders` - these control the flow of activity tasks in a workflow. If a step passes or fails in an SWF workflow, a decider `decides` what steps to do next, or to exit.
- `Activity Workers` - these actually do the work/tasks in the SWF workflow. A task could be something like call a particular SNS topic, create a new EC2 instance, or perform an Elastic Map Reduce (EMR) job