# Mermaid Demo

## Introduction

Demonstration of "Mermaid" diagramming tool - <https://mermaid.js.org/>

## Example Embedded Mermaid Diagram

Mermaid diagrams can be embedded directly into Markdown, and rendered
automatically by GitHub.

The following diagram attempts to replicate
<https://github.com/umd-lib/umd-fcrepo/blob/main/docs/img/MessagingSystem.svg>
using Mermaid.

```mermaid
flowchart TD
    User(((User)))
    ArchelonGui[Archelon Gui]
    PlastonHttpDaemon["Plastron HTTP Daemon"]
    PlastronCli[Plastron CLI]
    ArchelonStompListener[Archelon STOMP Listener]
    PlastronJobs[["plastron.jobs"]]
    PlastronJobsSynchronous[["plastron.jobs.synchronous"]]
    PlastronJobStatus[[plastron.job.status]]
    PlastronJobProgress[["[topic]\nplastron.job.progress"]]
    PlastronStompDaemon["Plastron STOMP Daemon"]
    Reindex[["reindex"]]
    Fcrepo["fcrepo"]
    Fedora[["fedora"]]
    Index[["index"]]
    FixityCandidates[["fixitycandidates"]]
    Fixity[["fixity"]]
    VarLogFixity[/"/var/log/fixity"\]
    LibFcrepoNotify[/"lib-fcrepo-notify@umd.edu"/]
    IndexSolr[["index.solr"]]
    IndexTripleStore[["index.triplestore"]]
    Audit[["audit"]]
    AuditTripleStore[["audit.triplestore"]]
    AuditDatabase[["audit.database"]]
    AuditDB[("Audit Database")]
    Fuseki(("Fuseki"))
    Solr(("Solr"))

    User-..->ArchelonGui
    User-..->PlastronCli
    ArchelonGui--"[HTTP] Get job status"-->PlastronJobs
    ArchelonGui--"[STOMP]"-->PlastronJobsSynchronous
    ArchelonGui-->PlastonHttpDaemon
    ArchelonStompListener--"[HTTP] Notification"-->ArchelonGui
    PlastronJobStatus--"[STOMP]"-->ArchelonStompListener
    PlastronJobProgress--"[STOMP]"-->ArchelonStompListener
    PlastronJobs--"[STOMP]"-->PlastronStompDaemon
    PlastronJobsSynchronous--"[STOMP]"-->PlastronStompDaemon
    PlastronStompDaemon--"[STOMP]"-->PlastronJobProgress
    PlastronStompDaemon--"[STOMP]"-->PlastronJobStatus
    PlastronCli--"[HTTP]\ncreate/update resources"-->Fcrepo
    PlastronCli--"[STOMP]"-->Reindex
    PlastronStompDaemon--"[HTTP]\ncreate/update resources"-->Fcrepo
    Fcrepo--"[JMS]"-->Fedora
    Reindex--"[JMS]"-->Index
    Fedora--"[JMS]"-->Index
    Fedora--"[JMS] /resource is binary/"-->FixityCandidates
    Fedora--"[JMS] /resource is binary/"-->Fixity
    Fedora--"[JMS]"-->Audit
    Audit--"[JMS]"-->AuditTripleStore
    Audit--"[JMS]"-->AuditDatabase
    Index--"[JMS]"-->IndexSolr
    Index--"[JMS]"-->IndexTripleStore
    AuditDatabase--"[SQL]"-->AuditDB
    Fixity-."/fixity check fails/".->LibFcrepoNotify
    Fixity-.->VarLogFixity
    IndexSolr--"[HTTP]"-->Solr
    AuditTripleStore--"[HTTP]"-->Fuseki
    IndexTripleStore--"[HTTP]"-->Fuseki
```

