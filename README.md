# If Related List Workflow Activity

ServiceNow's workflow editor can be useful when working with logic that may change often. One area that is lacking is the ability to work with records from related lists. This adds a new activity allowing you to have an If condition based upon values in a related list.

## Options

You are provided with 4 options when using the activity.

**Related Table:** The table that your condition will be applied to.

**Workflow Table Field:** The field that you are using to tie the *related table* to the table the workflow is for. This is going to be the *sys_id* in most cases.

**Related Table Field:** The field on the related table that will contain the value from the *workflow table field*

**Condition:** The condition that you are checking for.

## Example

![](http://i.imgur.com/Ur61s7b.png)

In this example we are looking at the Affected CIs for an Incident. The *Sys ID* from the Incident should match the value in the *Task* field on the *CIs Affected* table. We are then checking if the CI cost is more than 10,000.

## What is it doing?

The activity builds builds a query against the table given as the *Related Table*. The first parameter of the query is that the value in the *Workflow Table Field* matches the value for the *Related Table Field*. Then the *Condition* given is added as an encoded query. If any records are returned the the workflow follows the Yes branch, otherwise it follows the No branch.

Below is an example in code to give you a better idea:

```javascript
var gr = new GlideRecord('task_ci');
gr.addQuery('task',current.getValue('sys_id'));
gr.addEncodedQuery(condition);
gr.query();
```