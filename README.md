# Cheap n8n hosting: is a $21.99/year VPS enough, who fixes it when n8n breaks, and when should you pay more?

RackNerd's cheapest KVM VPS special costs $21.99 a year, about $1.83 a month for the machine n8n runs on. Two lines further down RackNerd's own page, n8n is listed as comfortable from 2 GB of RAM, which moves the realistic entry point to $35.99 a year. That $14 gap is the first decision in this article. The rest covers what the annual price does and does not include, the execution math that decides whether self-hosting saves anything at all, and the workload size at which a cheap VPS stops being the right answer.

> **Quick verdict:** Most people running n8n on a budget should start with the 2 GB KVM VPS at $35.99/year, with 2 vCores, 35 GB SSD and 5 TB of monthly transfer. It is the smallest plan that matches RackNerd's own stated memory requirement for n8n. The $21.99 plan is fine for testing workflows; it is thin for running them on a schedule.
>
> 👉 [Open the RackNerd VPS specials and pick the 2 GB plan](https://bit.ly/RacKnerd)

## Every RackNerd VPS plan that can run n8n

The specials page lists five KVM plans. All are annual, all come with full root SSH access, instant provisioning and a 1 Gbps port. Prices below are the yearly totals RackNerd quotes, with the monthly equivalent added so you can compare against hosts that advertise monthly.

| Plan | vCPU / RAM | SSD storage | Price (billed yearly) | Order |
| --- | --- | --- | --- | --- |
| 1 GB KVM VPS | 1 vCore / 1 GB | 20 GB | $21.99/year (~$1.83/mo) | [Order the 1 GB plan](https://bit.ly/RacKnerd) |
| 2 GB KVM VPS | 2 vCores / 2 GB | 35 GB | $35.99/year (~$3.00/mo) | [Order the 2 GB plan](https://bit.ly/RacKnerd) |
| 4 GB KVM VPS | 2 vCores / 4 GB | 60 GB | $59.99/year (~$5.00/mo) | [Order the 4 GB plan](https://bit.ly/RacKnerd) |
| 6 GB KVM VPS | 6 vCores / 6 GB | 100 GB | $89.99/year (~$7.50/mo) | [Order the 6 GB plan](https://bit.ly/RacKnerd) |
| 8 GB KVM VPS | 7 vCores / 8 GB | 150 GB | $119.99/year (~$10.00/mo) | [Order the 8 GB plan](https://bit.ly/RacKnerd) |

Two specs sit outside the table because they rarely decide an n8n purchase. Monthly transfer runs from 3,000 GB on the 1 GB plan up to 20,000 GB on the 8 GB plan. Workflow automation moves JSON between APIs, so you are unlikely to hit a transfer cap before you hit a memory ceiling. Storage is RAID-10 SSD across the range, which matters more than it sounds: n8n keeps workflow definitions, credentials and execution history in its database, and slow disk shows up as a slow editor.

RackNerd lists eleven locations for these plans: Los Angeles, San Jose, Seattle, Dallas, Atlanta, Chicago, New Jersey, New York, Ashburn, Amsterdam and France. Pick by where your APIs live, not by where you live. If half your nodes call a European CRM, Amsterdam or France cuts a round trip on every execution. If they call US services, stay in the US.

## The annual bill, and what it hides

A yearly figure is easier to read than a monthly one, and RackNerd shows the real number. Most cheap hosting pages do the opposite. A current example from the self-hosted n8n page at Hostinger: KVM 1 is headlined at $6.49/mo, but the line under it says you pay $155.76 today for 24 months, and it renews at $11.99/mo for the same term. Three different numbers for one plan, and only the middle one is what leaves your account at checkout.

RackNerd's page does not do that. What it also does not spell out in the plan table is the renewal rate and the refund window. Confirm both before you order. The renewal rate decides what year two costs, and the refund window decides how much of a mistake you are allowed to make in week one.

👉 [Check the annual total and plan details on RackNerd's order page](https://bit.ly/RacKnerd)

## What cheap n8n hosting actually replaces: the execution meter

n8n Cloud's Starter tier allows 2,500 executions a month at roughly $24 a month. A single workflow set to poll every five minutes fires 8,640 times a month on its own, which is three and a half times the Starter allowance before a second workflow exists. That is the pattern behind most people searching for cheap n8n hosting: the automation works, the bill tracks how often it runs, and adding a workflow feels like adding a subscription.

On a self-hosted instance the meter disappears. n8n Community Edition has no execution cap, no workflow cap and no user cap, and the only variable cost is the server. A 2 GB RackNerd plan at $35.99 a year sits against roughly $288 for a year of the cloud Starter tier. The saving is real, and it holds only while your workflows fit inside 2 GB.

## One-click install, and where support ends

n8n is one of the apps in RackNerd's ctrl panel. After the VPS deploys you open One-Click Apps, select n8n, and the login credentials appear in the panel when it is ready. That skips the Docker install and the reverse proxy, and it is the reason this plan is worth considering at all rather than any generic VPS.

Then the line appears. RackNerd describes these as unmanaged KVM VPS plans. You get root, and ctrl handles power, OS reinstall, an HTML5 console, one-click apps and a network firewall. Support is there 24/7 for the platform. Everything above the operating system is yours: n8n configuration, credentials, node setup, custom JavaScript, upgrades.

That boundary is normal across the category, and it is worth understanding before you buy rather than after. Hostinger states that its support covers the VPS environment and not internal n8n workflows, configuration or custom code. OVHcloud splits it the same way, with the infrastructure on their side and the OS, firewall and n8n application on yours.

If the maintenance is the part you want gone, a managed n8n host is the other trade. BearHost starts at $6.99/mo with PostgreSQL, automatic SSL and daily backups bundled, which works out to about $84 a year against $35.99. You are paying roughly $48 extra for someone else to own the n8n layer. Whether that is worth it depends entirely on whether you would rather debug a failed node or open a ticket.

👉 [Compare RackNerd's plan sizes and decide how much server to manage yourself](https://bit.ly/RacKnerd)

## Which plan fits your workflow volume

RackNerd's own guidance puts the n8n floor at 2 GB. Beyond that, size by count and frequency of workflows, plus whatever else shares the box.

- **A handful of low-frequency workflows, one user, SQLite:** 2 GB at $35.99 a year. Fits comfortably.
- **Dozens of workflows on active schedules, PostgreSQL on the same box:** 4 GB at $59.99 a year. The extra RAM is what PostgreSQL wants when n8n is writing execution records during runs.
- **Queue mode with Redis and separate workers, or AI nodes calling a model API on every execution:** 8 GB at $119.99 a year, and plan to move the database off the machine eventually.

Queue mode is an n8n feature you configure yourself. RackNerd gives you root and the RAM for it; there is no managed queue setup on the plan. On a single 4 GB box, running n8n, PostgreSQL and Redis together is workable for a small queue, and the moment you add a second worker you will want the 8 GB plan.

CPU matters less than the spec sheet suggests. Most n8n nodes spend their time waiting on an HTTP response, not computing. What runs out first under load is RAM, then disk throughput once execution history has been accumulating for a few months. Keep an eye on that on the 35 GB and 60 GB plans.

👉 [Start with the 4 GB plan if you are running PostgreSQL alongside n8n](https://bit.ly/RacKnerd)

## When cheap n8n hosting is the wrong buy

Four cases where paying less now costs more later.

**You need SSO, audit logs or credential encryption at rest.** Those are n8n Enterprise features. A $35.99 VPS does not provide them, and configuring an equivalent yourself is a project, not a checkbox.

**You need an SLA with financial backing.** These are unmanaged specials on single servers. There is no failover, and a host-level outage means your workflows stop until the node comes back.

**Nobody on the team will open a terminal.** The one-click install gets n8n running. It does not help when a workflow fails after an n8n upgrade, or when the database needs a backup restored.

**Your workflows are business-critical and silent when broken.** Self-hosting means you also own monitoring. n8n has error workflows you can wire to Slack or email; nobody sets that up for you.

## FAQ

**Do I have to install n8n myself?**
No. n8n is a one-click app in the ctrl panel. You still configure your own workflows afterward, and you own updates.

**Are executions really unlimited?**
n8n Community Edition does not meter executions, so RackNerd is not charging per run. Your ceiling is the server's RAM, CPU and disk.

**Can I install community nodes and custom code?**
Yes. These plans come with full root access, and n8n supports community nodes and custom JavaScript or Python inside workflows.

**Where does my data live?**
On your VPS, in the n8n database. Pick the datacenter closest to the services your workflows call.

**Do I need a separate database?**
Not to start. SQLite ships with n8n and works for light use. PostgreSQL on the same box is the usual next step, which is where the 4 GB plan earns its price.

**Monthly or annual?**
RackNerd quotes these plans yearly. There is no monthly option on the specials listed here, so the yearly total is the number that matters.

## How to decide at checkout

Match the plan to what your workflows do, not to the lowest price on the page. A few test workflows, or a single daily sync, and the 2 GB plan at $35.99 is enough; the 1 GB plan at $21.99 will boot n8n but leaves little room once PostgreSQL and execution history arrive. Running dozens of scheduled workflows with a database on the same machine, take the 4 GB at $59.99. Adding queue mode workers or AI nodes that fire on every execution, go to 8 GB at $119.99 and budget for moving the database off the box later.

Before paying, confirm two things on the order page: the renewal rate for the term after this one, and the refund window. Both decide what happens if the plan you picked turns out to be the wrong size.

👉 [See the full RackNerd VPS specials list and order the plan that fits](https://bit.ly/RacKnerd)
