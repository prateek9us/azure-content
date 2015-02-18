The Challenge
=============

Email is one of the most critical applications that is required for a
business to function. Business of all sizes depend upon the email to
communicate with team members, other teams in the organizations,
vendors, customers et al. Unavailability of email can bring a business
to a halt. Therefore it is of utmost importance that the business
ensures that the email infrastructure is resilient and is protected
against all forms of disasters.

Microsoft Exchange is the most popular software that enterprises use to
host their email services. Microsoft Exchange natively supports a
Database Availability Group (DAG) which can enable high availability. A
DAG can also be extended to a remote site to provide disaster recovery.

To achieve the capability of disaster recovery, the solution based on
DAG requires that you always run active instances on the recovery site.
This implies that you would need to spend not only to run the instances
on the remote site but also for the licenses to run those instances.

If you are a small enterprise and don’t already have an active remote
site, always running active instances can turn out to be very expensive.

The Solution
============

Azure Site Recovery provides disaster recovery by using a cold remote
site. Virtual Machines are bought up on the recovery site only in the
event of a failover. Not only this, Azure Site Recovery also helps you
orchestrate the end to end failover by providing you following
capabilities:

-   Ordering the shutdown and start up sequence of different roles of
    the Microsoft Exchange Server

-   Providing capability to run scripts as part of recovery flow

-   Adding Manual Action between different steps of recovery so that you
    can validate actions before moving to the next steps or manually
    accomplishing the recovery steps that you have not yet automated

-   Configuring networking for the failed over virtual machine

    ![](media/image1.png)

    The diagram above shows the setup for an SMB customer contoso.com
    who has two node Microsoft Exchange 2013 setup without using DAG.
    Domain controller and both the nodes of Exchange, CAS and MBX, are
    being replicated to the remote site using one of the many
    replication channels supported by Azure Site Recovery.

    Azure Site Recovery not only sets up the replication between the two
    sites but also allows you to failover to a different network subnet
    on the recovery site. Azure Site Recovery changes the IP
    configuration of the failed over virtual machines based on the
    network settings of the recovery site.

    Azure Site Recovery greatly simplifies the protection and recovery
    process for Microsoft Exchange

About Azure Site Recovery
=========================

Azure Site Recovery an Azure based service that provides disaster
recovery capabilities by orchestrating replication, failover and
recovery of virtual machines in a number of deployment scenarios.

You can [check out additional product
information](http://aka.ms/sol_productinfo), and [sign-up for a free
Azure trial](http://aka.ms/sol_trial) to start trying out Microsoft
Azure using Azure Site Recovery.

If you have any questions, please visit the [Azure Site Recovery forum
on MSDN](http://aka.ms/sol_forum) for additional information and to
engage with other customers.
