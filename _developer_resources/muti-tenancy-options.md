---
title: Multi-Tenancy Options
layout: page
---

If you don't have the resources (or the cash flow, or the unit economics) to support single-tenant everything. You'll need multi-tenant application servers and multi-tenant database servers. [The available options for this are row-level isolation, schema-level isolation, and database-level isolation](https://blog.arkency.com/comparison-of-approaches-to-multitenancy-in-rails-apps/).

- Row-level isolation can be called "intermingling data". However, [Postgres has Row Level Security (RLS)](https://aws.amazon.com/blogs/database/multi-tenant-data-isolation-with-postgresql-row-level-security/), which *may* be good enough for usage, especially initially.  [Dovetail, for example, has their SOC2 Type I, working on Type II, and is using RLS](https://dovetailapp.com/security/). There's some articles talking about the approach: [https://pganalyze.com/blog/postgres-row-level-security-ruby-rails](https://pganalyze.com/blog/postgres-row-level-security-ruby-rails)
- Schema-level isolation is used by the apartment gem, but [Heroku strongly recommends against it](https://devcenter.heroku.com/articles/heroku-postgresql#multiple-schemas). [The authors of the apartment gem no longer recommend that approach,](https://influitive.io/our-multi-tenancy-journey-with-postgres-schemas-and-apartment-6ecda151a21f) and there's [a good blog post going into much more detail](https://dev.to/matiascarpintini/multi-tenant-apps-on-ruby-on-rails-5f49). Both of these recommend row-level isolation. [There's some discussion on Hacker News, too](https://news.ycombinator.com/item?id=23305111).
    
    > Although there are situations where a schema-per-tenant approach is not ideal, it is a good option for many use cases as it provides a good mix of data isolation, cross-container query capability, application schema customizability, shared administration, and shared resource usage. This option is well-suited for a moderate number of tenants with a moderate set of tables in each application schema. Serving the middle ground, this option is often chosen as a starting point when requirements and long-term needs do not clearly point to using one of the other options.
    > 
- Database-level isolation is not administratively feasible or cost effective for us at this time.

Patrick McKenzie specifically says:

> I am aware of at least one company which does this from my consulting days, and would caution you that what you get in perceived security benefits from making sure that tenants can't interact with each others' data you'll give back many times over with engineering complexity, operational issues, and substantial pain to resolve ~trivial questions.
I also tend to think that the security benefit is more theatre than reality. If an adversary compromises an employee laptop or gets RCE on the web tier (etc, etc), they'll get all the databases regardless of whose account (if any) they started with.
- [https://news.ycombinator.com/item?id=23308945](https://news.ycombinator.com/item?id=23308945)
> 

The advantage of row level security is that it can easily be split up into separate schemas or databases, while split databases would have to deal with conflicting IDs and other uniqueness if you want to later combine them. So RLS is more of a reversible decision than others.
