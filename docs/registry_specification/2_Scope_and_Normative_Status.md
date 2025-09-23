# Scope and Normative Status

The scope of this document is to specify the logical interfaces for the
SDMX registry in terms of the functions required and the data that may
be present in the function call, and the behaviour expected of the
registry.

In this document, functions and behaviours of the Registry Interfaces
are described in four ways:

- in text
- with tables
- with UML diagrams excerpted from the SDMX Information Model
    (SDMX-IM)
- with UML diagrams that are not a part of the SDMX-IM but are
    included here for clarity and to aid implementations (these diagrams
    are clearly marked as “Logical Class Diagram ...”)

Whilst the introductory section contains some information on the role of
the registry, it is assumed that the reader is familiar with the uses of
a registry in providing shared metadata across a community of
counterparties.

Note that chapters 5 and 6 below contain normative rules regarding the
Registry Interface and the identification of registry objects. Further,
the minimum standard for access to the registry is via a REST interface
(HTTP or HTTPS), as described in the appropriate sections. The
notification mechanism must support e-mail and HTTP/HTTPS protocols as
described. Normative registry interfaces are specified in the SDMX-ML
specification (Section 3 of the SDMX Standard). All other sections of
this document are informative.

Note that although the term “authorised user” is used in this document,
the SDMX standards do not define an access control mechanism. Such a
mechanism, if required, must be chosen and implemented by the registry
software provider.