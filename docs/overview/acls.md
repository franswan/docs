---
sidebar_position: 4
---

# Access Control
NetBird allows administrators to restrict access to resources (peers) by creating access rules and
defining what peer groups are permitted to establish connections with one another.

<div class="videowrapper">
<iframe src="https://www.youtube.com/embed/WvbkACjdsHA" allow="fullscreen;"></iframe>
</div>

## Introduction
A NetBird account comes with a `Default` rule that allows all peers of the account to connect to each other forming a full mesh network.
In most cases, this is the desired state for a small network or network that has low-security requirements.
When you need to restrict access to certain resources that belong to specific users or services within your organization, you can create rules that dictate who can access what.

Access control rules make use of groups to control connections between peers; these groups can be added as `Source` or `Destination` of a rule and will be evaluated when the Management service distributes the list of peers across your network.

## Concepts
### Groups
A NetBird group works and follows a similar concept to tags in other platforms; they are easily created and can be associated with peers and used in rules to control traffic within your network.

Some characteristics of groups:
- They are unique.
- One group can have multiple peers.
- Peers can belong to multiple groups.
- Rules can have multiple groups in their `Source` and `Destination` lists.
- They are created in the `Access Control` or `Peers` tabs.
- They can only be deleted via API.
- There is a default group called `All`.

### The All Group
The `All` group is a default group to which every peer in your network is automatically added to. This group cannot be modified or deleted.
### Rules
Rules are lists of `Source` and `Destination` groups of peers that can communicate with each other.
Rules are processed when the Management service distributes a network map to all peers of your account. Because you can only create ALLOW rules, there is no processing
order or priority, so the decision to distribute peer information is based on its association with a group belonging to an existing rule.

Currently, the communication between lists of groups in source and destination lists of a rule is bidirectional,
meaning that destinations can also initiate connections to a group of peers listed in the source field of the rule.

The behavior of a network without any rules is to deny traffic. No peers will be able to communicate with each other.

:::tip
If you need to allow peers from the same group to communicate with each other, just add the same group to the `Source` and `Destination` lists.
:::

### The Default Rule
The `Default` rule is created when you first create your account. This rule is very permissive because it allows communication between all peers in your network. 
It uses the [`All`](#the-all-group) group as a source and destination. If you want to have better 
control over your network, it is recommended that you delete this rule and create more restricted rules with custom groups.

:::tip
If you need to restrict communication within your network, you can create new rules and use different groups, and then remove the default rule to achieve the desired behavior.
:::

### Multiple Mesh Networks
As mentioned above, rules are bidirectional, which is basically the control of how your network will behave as a mesh network. 

There is a `Default` rule, which configures a Default mesh connection between all peers of your network. With rules, you can define smaller mesh networks by grouping peers and adding these groups to `Source` and `Destination` lists. 
## Managing Rules

### Creating Rules
After accessing the `Access Control` tab, you can click on the `Add Rule` button to create a new rule. This will open a screen 
where you need to name the rule, set its status, and add groups to the source and destination lists.

<p align="center">
    <img src="/docs/img/overview/create-rule.png" alt="high-level-dia" width="300" style={{boxShadow: '0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)'}} />
</p>

If required, you can create new groups by simply entering new names in the input box for either source or destination lists.

<p align="center">
    <img src="/docs/img/overview/create-group-in-rule.png" alt="high-level-dia" width="300" style={{boxShadow: '0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)'}} />
</p>

Once you are done configuring the rule, click the `Create` button to save it. You will then see your new rule in the table.
<p align="center">
    <img src="/docs/img/overview/new-rule-list.png" alt="high-level-dia" width="600" style={{boxShadow: '0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)'}} />
</p>

:::caution Reminder
Because of its permissiveness, new rules will take effect once you remove the `Default` rule.
:::

#### Adding peers to groups
If you create a new group when defining a rule, you will need to associate peers with this group. 
You can do it by accessing the `Peers` tab and clicking the `Groups` column of any peer you want to associate with the new group. 

<p align="center">
    <img src="/docs/img/overview/associate-peer-groups.png" alt="high-level-dia" width="300" style={{boxShadow: '0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)'}} />
</p>

### Updating Rules
To update a rule, you can click on the rule's `Name` or on either `Sources` and `Destinations` columns. You could also click the menu 
button of a rule and select `View`. This will open the same screen where you can update rule groups, description, or status.
### Disabling Rules
To disable a rule, you should follow the steps of [updating rules](#updating-rules) changing its status, and then click on Save.
### Deleting Rules
To delete a rule, you should click on the rule's menu and choose `Delete`. A confirmation window will pop up.

<p align="center">
    <img src="/docs/img/overview/delete-rule-menu.png" alt="high-level-dia" width="600" style={{boxShadow: '0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)'}} />
</p>

<p align="center">
    <img src="/docs/img/overview/delete-rule-popup.png" alt="high-level-dia" width="300" style={{boxShadow: '0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)'}} />
</p>
