# 5 Registry Interfaces and Services

## 5.1 Registry Interfaces

The Registry Interfaces are:

- Notify Registry Event
- Submit Subscription Request
- Submit Subscription Response
- Submit Registration Request
- Submit Registration Response
- Query Registration Request
- Query Registration Response
- Query Subscription Request
- Query Subscription Response

The registry interfaces are invoked in one of two ways:

1. The interface is the name of the root node of the SDMX-ML document
2. The interface is invoked as a child element of the RegistryInterface
    message where the RegistryInterface is the root node of the SDMX-ML
    document.

In addition to these interfaces the registry must support a mechanism
for submitting and querying for structural metadata. This is detailed in
sections 5.2.2 and 5.2.3.

All these interactions with the Registry – with the exception of
NotifyRegistryEvent – are designed in pairs. The first document, the one
which invokes the SDMX-RR interface, is a “Request” document. The
message returned by the interface is a “Response” document.

It should be noted that all interactions are assumed to be synchronous,
with the exception of Notify Registry Event. This document is sent by
the SDMX-RR to all subscribers whenever an even occurs to which any
users have subscribed. Thus, it does not conform to the request-response
pattern, because it is inherently asynchronous.

## 5.2 Registry Services

### 5.2.1 Introduction

The services described in this section do not imply that each is
implemented as a discrete web service.

### 5.2.2 Structure Submission Service

The registry must support a mechanism for submitting structural
metadata. This mechanism can be the SDMX REST interface for structural
metadata (this is defined in the corresponding GitHub project, dedicated
to the SDMX REST API: <https://github.com/sdmx-twg/sdmx-rest>). In order
for the architecture to be scalable, the finest-grained piece of
structural metadata that can be processed by the SDMX-RR is a
MaintainableArtefact, with the exception of Item Schemes, where changes
at an Item level is also possible (see next section on the SDMX
Information Model).

### 5.2.3 Structure Query Service 

The registry must support a mechanism for querying for structural
metadata. This mechanism can be the SDMX REST interface for structural
metadata (this is defined in the corresponding GitHub project, dedicated
to the SDMX REST API: <https://github.com/sdmx-twg/sdmx-rest>). The
registry response to this query mechanism is the SDMX Structure message,
which has as its root node:

- Structure

The SDMX structural artefacts that may be queried are:

- data flows and metadata flows
- data structure definitions and metadata structure definitions
- code lists
- value lists
- concept schemes
- reporting taxonomies
- provision agreements and metadata provision agreements
- structure maps
- representation map
- organisation scheme map
- concept scheme map
- category scheme map
- reporting taxonomy map
- processes
- hierarchies
- constraints
- category schemes
- categorisations and categorised objects (examples are categorised
    data flows and metadata flows, data structure definitions, metadata
    structure definitions, provision agreements registered data sources
    and metadata sources)
- organisation schemes (agency scheme, data provider scheme, data
    consumer scheme, organisation unit scheme)

Due to the VTL implementation the other structural metadata artefacts
that may be queried are:

- Transformation schemes
- Custom type schemes
- Name personalisation schemes
- VTL mapping schemes
- Ruleset schemes
- User defined operator schemes

### 5.2.4 Data and Reference Metadata Registration Service 

This service must implement the following Registry Interfaces:

- SubmitRegistrationRequest
- SubmitRegistrationResponse
- QueryRegistrationRequest
- QueryRegistrationResponse

The Data and Metadata Registration Service allows SDMX conformant files
and web-accessible databases containing published data and reference
metadata to be registered in the SDMX Registry. The registration process
MAY validate the content of the datasets or metadata-sets, and MAY
extract a concise representation of the contents in terms of concept
values (e.g., values of the data attribute, dimension, metadata
attribute), or entire keys, and storing this as a record in the registry
to enable discovery of the original dataset or metadata-set. These are
called Constraints in the SDMX-IM.

The Data and Metadata Registration Service MAY validate the following,
subject to the access control mechanism implemented in the Registry:

- that the data/metadata provider is allowed to register the dataset
    or metadataset;
- that the content of the dataset or metadataset meets the validation
    constraints. This is dependent upon such constraints being defined
    in the structural repository and which reference the relevant
    Dataflow, Metadataflow, Data Provider, Metadata Provider, Data
    Structure Definition, Metadata Structure Definition, Provision
    Agreement, Metadata Provision Agreement;
- that a queryable data source exists – this would necessitate the
    registration service querying the service to determine its
    existence;
- that a simple data source exists (i.e., a file accessible at a URL);
- that the correct Data Structure Definition or Metadata Structure
    Definition is used by the registered data;
- that the components (Dimensions, Attributes, Measures, Metadata
    Attributes, etc.) are consistent with the Data Structure Definition
    or Metadata Structure Definition;
- that the valid representations of the concepts to which these
    components correspond conform to the definition in the Data
    Structure Definition or Metadata Structure Definition.

The Registration has an action attribute which takes one of the
following values:

| <strong>Action Attribute Value</strong> | <strong>Behaviour</strong> |
| :--- | :--- |
| Append | Add this registration to the registry |
| Replace | Replace the existing Registration with this Registration identified<br>by the id in the Registration of the Submit Registration Request |
| Delete | Delete the existing Registration identified by the id in the<br>Registration of the Submit Registration Request |


The Registration has three Boolean attributes which may be present to
determine how an SDMX compliant dataset or metadataset indexing
application must index the datasets or metadatasets upon registration.
The indexing application behaviour is as follows:

| <strong>Boolean Attribute</strong> | <strong>Behaviour if Value is “true”</strong> |
| :--- | :--- |
| indexTimeSeries | A compliant indexing application must index all the time series keys<br>(for a Dataset registration) or metadata target values (for a<br>Metadataset registration) |
| indexDataSet | <p>A compliant indexing application must index the range of actual<br>(present) values for each dimension of the Dataset (for a Dataset<br>registration) or the range of actual (present) values for each Metadata<br>Attribute which takes an enumerated value.</p><br><p>Note that for data this requires much less storage than full key<br>indexing, but this method cannot guarantee that a specific combination<br>of Dimension values (the Key) is actually present in the<br>Dataset</p> |
| indexReportingPeriod | A compliant indexing application must index the time period range(s)<br>for which data are present in the Dataset. The validity period of the<br>Metadatasets may also be indexed. |


### 5.2.5 Data and Reference Metadata Discovery

The Data and Metadata Discovery Service implements the following
Registry Interfaces:

- QueryRegistrationRequest
- QueryRegistrationResponse

### 5.2.6 Subscription and Notification

The Subscription and Notification Service implements the following
Registry Interfaces:

- SubmitSubscriptionRequest
- SubmitSubscriptionResponse
- NotifyRegistryEvent

The data sharing paradigm relies upon the consumers of data and metadata
being able to pull information from data providers’ dissemination
systems. For this to work efficiently, a data consumer needs to know
when to pull data, i.e., when something has changed in the registry
(e.g., a dataset has been updated and re-registered). Additionally, SDMX
systems may also want to know if a new Data Structure Definition, Code
List or Metadata Structure Definition has been added. The Subscription
and Notification Service comprises two parts: subscription management,
and notification.

Subscription management involves a user submitting a subscription
request which contains:

- a query or constraint expression in terms of a filter which defines
    the events for which the user is interested (e.g., new data for a
    specific dataflow, or for a domain category, or changes to a Data
    Structure Definition).
- a list of URIs or endpoints to which an XML notification message can
    be sent. Supported endpoint types will be email (mailto:) and HTTP
    POST (a normal http:// address);
- request for a list of submitted subscriptions;
- deletion of a subscription;

Notification requires that the structural metadata repository and the
provisioning metadata repository monitor any event which is of interest
to a user (the object of a subscription request query), and to issue an
SDMX notification document to the endpoints specified in the relevant
subscriptions.

### 5.2.7 Registry Behaviour

The following table defines the behaviour of the SDMX Registry for the
various Registry Interface messages. It should be noted, though, that as
of SDMX 3.0, an extended versioning scheme newly including semantic
versioning is foreseen for all Maintainable Artefacts. Moreover, while
the old versioning scheme is allowed, given there is no more a "final"
flag, there is no way guaranteeing the consistency across version of a
Maintainable, unless semantic versioning is used.

Given the above, the behaviour described in the following table concerns
either draft Artefacts using semantic versioning or any Artefacts using
the old versioning scheme. Nevertheless, in the case of semantic
versioning the registry must respect the versioning rules when
performing the actions below. For example, it is not possible to replace
a non-draft Artefact that follows semantic versioning, unless a newer
version is introduced according to the semantic versioning rules.
Furthermore, even when draft Artefacts are submitted, the registry has
to verify semantic versioning is respected against the previous
non-draft versions. It is worth noting that the rules for semantic
versioning and replacing or maintaining semantically versioned Artefacts
applies to externally shared Artefacts. This means that any system may
internally perform any change within a version of an Artefact, until the
latter is shared outside of that system or becomes public. Then (as also
explained in the SDMX Standards Section 6 “Technical Notes”) the
Artefacts must adhere to the Semantic Versioning rules.

| <strong>Interface</strong> | <strong>Behaviour</strong> |
| :--- | :--- |
| All | <ol type="1"><br><li><p>If the action is set to “replace” (or a maintainable Artefact is<br>PUT or POSTed) then the entire contents of the existing maintainable<br>object in the Registry MUST be replaced by the object<br>submitted.</p></li><br><li><p>Cross referenced structures MUST exist in either the submitted<br>document (in Structures or Structure Location) or in the registry to<br>which the request is submitted.</p></li><br><li><p>If the action is set to “delete” (or a maintainable Artefact is<br>DELETEd) then the Registry MUST verify that the object can be deleted.<br>In order to qualify for deletion, the object must:</p><br><ol type="a"><br><li><p>Be a draft version.</p></li><br><li><p>Not be explicitly[^1] referenced from any other object in<br>the Registry.</p></li><br></ol></li><br><li><p>The semantic versioning rules in the SDMX documentation MUST be<br>obeyed.</p></li><br></ol> |
| Structure submission | Structures are submitted at the level of the Maintainable Artefact<br>and the behaviour in “All” above is therefore at the level of the<br>Maintainable Artefact. |
| SubmitRegistrationRequest | <p>If the datasource is a file (simple datasource) then the file MAY<br>be retrieved and indexed according to the Boolean attributes set in the<br>Registration.</p><br><p>For a queryable datasource the Registry MAY validate that the source<br>exists and can accept an SDMX data query.</p> |

[^1]:
    With semantic versioning, it is allowed to reference a
    range of artefacts, e.g., a DSD referencing a Codelist with version
    1.2.3+ means all patch versions greater than 1.2.3. This means that
    deleting 1.2.4-draft does not break integrity of the aforementioned
    DSD.