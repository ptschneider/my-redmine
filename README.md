# my-redmine

I think of redmine as a FOSS alternative to Atlassian Confluence/JIRA. I need this if I have a large project with lots of components and external stakeholders.

Although redmine can display Gannt-formatted data, it has no resemblance to Micro$oft Project. If you are looking for a M$ Project clone, this aint the droid you're looking for.

## Why do I want this?

First, consider the use of gitlab-ce for a project.

Although you can manage a project with git shell scripts, the project will reach a maturity level where that becomes painful. With a tool like gitlab-ce, managing multiple versions of product undergoing different lifecycle transitions on a team with multiple people becomes a lot easier. For the developers actively working on the codebase.

For managers, success neither begins nor ends with coding tasks. There's analysis & design work prerequisite for any coding; there's support and impact analysis after the coding is done. git or gitlab-ce has too much low-level detail and not enough correlation with group activities, milestones, and higher-order processes.

So, you create a second activity/issue-tracking/reporting tier, using Atlassian, redmine, etc. Whereas gitlab-ce is configured to organize projects around system components, with the 'upper' layer (e.g. redmine) you would configure it to be organized around business outcomes, business milestones, business programs. These transcend any particular hardware/software asset, and may refer to different assets over time depending on how leaders are aggregating them to address business requirements. In that context, all pre-coding and post-coding tasks need to have a *separate* system for declaration/tracking than the system used to manage discrete code assets, because they are all correlated to non-code business metrics.

Or to put another way, you don't want non-developers forming opinions about the program based on what they read and half-understood in your developer's git write-ups. You'll spend all your time clearing up misunderstandings.

Critics say its just two parallel systems written for different audiences. That may have merit, but in-practice I've found the approach effective on larger longer-lived projects.

## Config

Offical docs only advertise support for MySQL & Postgres but mariadb seems ok so far.

default login is admin/admin

Think you can just login now, create a project and create an issue?

Oh no, Pollyanna, free software requires some sweat equity...

### User Roles

you must create a role before you can add ANY user to ANY new project

One approach:
 - keep site 'admin' account uniquely privileged for create/delete/open/close toplevel projects.
 - create 'contributor' role that can change most anything on a project their assigned to
 - create 'consultant' role that can view most anything but not change it

There is considerable more configuration applicable, depending upon your business processes & roles. 

A <10-person team doing 2-week Agile sprints and all their own analysis & design, testing and deployments-weekly will setup things different from a >20-person team supported by external system-engineering/test/deployment teams running on a different schedule. Kanban would be different for either. You'll set it up different depending on the last airline magazine your CTO read. You're already protected. Be grateful for the sandbox so 'e's not mucking about in your gitlab.

### Issue Priorities

Look under Enumerations. Create two: urgent, non-urgent. Those are the only two priorities anyone really appreciates anyway.

### Issue Categories

Nothing is provided by-default. In my example, the following handful of categories is adequate:

 - Business Program
 - Business Project
 - Milestone
 - Feature
 - Enhancement
 - Analysis
 - Specification
 - Design
 - Implementation
 - Problem
 - Verification
 - Validation

In practice, the top two here should always make intuitive sense to your non-tech folks, while the bottom two are where you link to associated git/gitlab tickets.  To illustrate further:

 - Business Programs & Projects should reflect non-tech business stakeholder perspective, objectives & priorities. This list should always align well with business sponsor's worldview, and amend it when it drifts. Write a Feature ticket to complain about tech debt.
 - Milestones & Problems are not unique to tech or non-tech perspectives, create/use them as makes sense.
 - One Feature ticket, to be successfully closed, requires one-or-more of Analysis-Specification-Design tickets, plus one-or-more EACH of Implmentation-Verification-Validation tickets.
 - An Enhancement is a Feature that requires no Analysis-Specification-Design tickets but still requires Implmentation-Verification-Validation tix. Should be something you can finish fast, not expected to be disruptive.  
 - Verification: did we build the product right? test suite created & passed? nerds happy?
 - Validation: did we build the right product? is ops happy? business stakeholder sign-off, inter-office memorandum

### Issue Statuses
Here's my list:

 - Created
 - Approved
 - Cancelled
 - Completed
 - Scheduled
 - Superceded
 - Suspended

### Trackers

Redmine quirk: issues must be associated with a Tracker, which in turn is associated with a Role via a Workflow.

Create one tracker called 'Backlog'. Anytime a new issue is created, it goes on the backlog, you're already busy.

You'll create other trackers as necessary, e.g. sprint name or release name. A team doing fixed quarterly sprints might name trackers 'CY24Q3' ... 'CY24Q4', another doing kanban with named releases might have 'galethread.00', depends on the team.

### Workflow

If you've entered everything up to this point, select Workflow.

A Workflow is a mapping of Role and Issue Status. This is to implement rules like, only a Manager can Approve a ticket.

This will be needed on a mature program, and you'll know how to tailor it once its absolutely needed. Start out with a simple approach.

Select contributor role, expand everything. Should be three big sections of checkboxes. Check them All. You'll figure out later what you need to restrict, but starting out just enable everything and move on.

Now you have a worklflow for issue status, you have a default status defined, you are ready to create an issue. 








