# Introduction

The business vision for SDMX envisages the promotion of a “data sharing”
model to facilitate low-cost, high-quality statistical data and metadata
exchange. Data sharing reduces the reporting burden of organisations by
allowing them to publish data once and let their counterparties “pull”
data and related metadata as required. The scenario is based on:

- the availability of an abstract information model capable of
    supporting time series and cross-sectional data, structural
    metadata, and reference metadata (SDMX-IM)
- standardised XML and JSON schemas for the SDMX-ML and SDMX-JSON
    formats derived from the model (XSD, JSON)
- the use of web-services technology (XML, JSON, Open API)

Such an architecture needs to be well organised, and the SDMX
Registry/Repository (SDMX-RR) is tasked with providing structure,
organisation, and maintenance and query interfaces for most of the SDMX
components required to support the data sharing vision.

However, it is important to emphasise that the SDMX-RR provides support
for the submission and retrieval of all SDMX structural metadata and
provisioning metadata. Therefore, the Registry not only supports the
data-sharing scenario, but this metadata is also vital in order to
provide support for data and metadata reporting/collection, and
dissemination scenarios.

Standard formats for the exchange of aggregated statistical data and
metadata as prescribed in SDMX v3.1 are envisaged to bring benefits to
the statistical community because data reporting and dissemination
processes can be made more efficient.

As organisations migrate to SDMX enabled systems, many XML, JSON (and
conventional) artefacts will be produced (e.g., Data Structure, Metadata
Structure, Code List and Concept definitions – often collectively called
structural metadata – XML schemas generated from data structure
definitions, XSLT stylesheets for transformation and display of data and
metadata, terminology references, etc.). The SDMX model supports
interoperability, and it is important to be able to discover and share
these artefacts between parties in a controlled and organized way.

This is the role of the registry.

With the fundamental SDMX standards in place, a set of architectural
standards are needed to address some of the processes involved in
statistical data and metadata exchange, with an emphasis on maintenance,
retrieval and sharing of the structural metadata. In addition, the
architectural standards support the registration and discovery of data
and referential metadata.

These architectural standards address the ‘how’, rather than the ‘what’,
and are aimed at enabling existing SDMX standards to achieve their
mission. The architectural standards address registry services, which
initially comprise:

- structural metadata repository
- data and metadata registration
- query

The registry services outlined in this specification are designed to
help the SDMX community manage the proliferation of SDMX assets and to
support data sharing for reporting and dissemination.