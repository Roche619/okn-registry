---
template: overrides/kg.html
shortname: medical-device-kg
title: Medical Device Knowledge Graph
description: Public FDA medical-device data in one linked graph, covering clearances and approvals, UDI device records, MAUDE and legacy adverse events, recalls, inspections and compliance actions, warning letters, establishments, standards, guidance, and 21 CFR.
stats: https://registry.okn.us/kg-stats/medical-device-kg
homepage: https://bmedesign.org/knowledgegraph
sparql: https://apps.okn.us/medical-device-kg/sparql
tpf: https://apps.okn.us/kgf/medical-device-kg/latest/tpf
kgf: https://apps.okn.us/kgf/medical-device-kg
license: "https://creativecommons.org/publicdomain/zero/1.0/"
funding:
  - https://www.nsf.gov/awardsearch/show-award/?AWD_ID=2535091
  - https://reporter.nih.gov/project-details/11261252
frink-options:
  lakefs-repo: medical-device-kg
  documentation-path: medical-device-kg
  kgf:
    semantics:
      prefixes:
        mdkg: "https://bmedesign.org/medical-device-kg/ns/"
        mdkg-id: "https://bmedesign.org/medical-device-kg/id/"
      roles:
        label:
          - "http://www.w3.org/2000/01/rdf-schema#label"
          - "https://bmedesign.org/medical-device-kg/ns/deviceName"
          - "https://bmedesign.org/medical-device-kg/ns/name"
      authoritative_namespaces:
        - mdkg
        - mdkg-id
contacts:
  - email: RocheRey.C.DeGuzman@hofstra.edu
    github: Roche619
    label: "Dr. Roche C. de Guzman"
  - email: Marco.Romanelli@hofstra.edu
    github: marcoromanelli-github
    label: "Dr. Marco Romanelli"
  - email: psingh37@pride.hofstra.edu
    github: Prabhadeus
    label: Prabhjot Singh
  - email: mbukhari1@pride.hofstra.edu
    github: MustafaSBny
    label: Mustafa Bukhari
---
<!-- Placeholders to fill after the final v0.0.7 re-test, then delete this comment: {{TRIPLES}} total triples (for example "1.9 billion"); {{RELEASE_DATE}} month and year of the v0.0.7 upload; {{MAUDE_REPORTS}} MAUDE reports (millions); {{UDI_RECORDS}} GUDID device records (millions); {{RECALLS}} recalls in the recall database; {{RECALL_CLASS_PCT}} percent of recalls with a recall class. -->
The Medical Device Knowledge Graph converts public U.S. Food and Drug Administration (FDA) device data into one linked RDF graph of about {{TRIPLES}} triples (release v0.0.7, {{RELEASE_DATE}}). Release v0.0.7 adds the remaining databases on FDA's Medical Device Databases page and related FDA device sources.

**Premarket and classification.** Product classification, with the detail fields from each product code page; radiation-emitting electronic product codes; 510(k) clearances, with links to the 510(k) summary PDFs; De Novo decisions and detail pages; PMA approvals and supplements; PMA review memos for 180-day design changes; Humanitarian Device Exemptions; Devices@FDA decisions; the AI-enabled medical devices list; device Emergency Use Authorizations; qualified Medical Device Development Tools; and advisory committee and panel meetings (archive to 2009).

**Postmarket safety.** The full MAUDE adverse-event history ({{MAUDE_REPORTS}} reports) with scrubbed event narratives; legacy MDR reports from 1984 to 1997; MAUDE Alternative Summary Reports (1999 to 2019); MedSun reports; recall enforcement reports and the recall database ({{RECALLS}} recalls, {{RECALL_CLASS_PCT}} with a recall class); Total Product Life Cycle data from FDA's TPLC pages and from MAUDE, premarket and recall counts per product code and year; Section 522 postmarket studies and Post-Approval Studies; safety communications and letters to health care providers; and the device shortage and discontinuance lists.

**Firms, compliance, and standards.** Establishment registration and listing; the Global Unique Device Identification Database ({{UDI_RECORDS}} device records); FDA Data Dashboard inspection classifications, inspection citations, compliance actions, and import refusals; device warning letters from 2005 onward; CDRH export certificates (CECV); recognized consensus standards; ASCA accredited testing laboratories and accreditation bodies; 510(k) third-party review organizations; CDRH and CBER device guidance documents; CLIA test categorizations; home-use IVD tests; mammography facilities; X-ray assembler reports; and all of Title 21 of the Code of Federal Regulations.

Records that fda.gov no longer serves (warning letters 2005 to April 2019, safety communications 2011 to 2022, discontinuances 2020 to 2024) are read from FDA's official web archive; each carries the archive URL, the original fda.gov URL, and a data-quality note.

Records join through shared nodes: FDA product code, regulation number, firm (FEI number), and device identifier (UDI-DI). Recall product descriptions that quote a GS1 barcode are linked to the matching UDI device record, so a recall can be traced to specific catalog items. Inspections, citations, compliance actions, and import refusals link to the firm by FEI number; citations, warning letters, and guidance documents link to the 21 CFR sections they cite; import refusals link to the device product code where FDA's import code contains one. Establishments carry Census geocodes, and product codes are mapped to NAICS industries. Vocabulary terms are under `https://bmedesign.org/medical-device-kg/ns/` and instances under `https://bmedesign.org/medical-device-kg/id/`.

Personal details are removed from narrative text (MAUDE, legacy MDR, MedSun, advisory meetings); MAUDE narratives are released only in scrubbed form. Contact persons are not ingested from any source, and Data Dashboard firms whose names identify an individual keep no name, address, or FEI number. The graph supports device safety surveillance, recall and adverse-event analysis, regulatory and compliance research, and teaching in biomedical engineering design.

**Main classes and keys.** `mdkg:RecallRecord` (recall number, `mdkg:recallClassification` "Class I/II/III", initiation and termination dates, root cause, `mdkg:codeInfo` lot text), `mdkg:MAUDEReport`, `mdkg:UDIDeviceRecord` and `mdkg:UDIIdentifier` (UDI-DI in `mdkg:identifierId`), `mdkg:K510Record`, `mdkg:PMARecord`, `mdkg:ProductCode` (FDA three-letter code in `mdkg:productCode`), `mdkg:Manufacturer` (FDA FEI number), `mdkg:RegistrationListingRecord` (registered establishments), `mdkg:TPLCRecord` (totals per product code), `mdkg:WarningLetter`, and `mdkg:GuidanceDocument`. Recalls link to devices through `mdkg:hasProductCode`, `mdkg:relatedK510Record`, `mdkg:relatedPMARecord`, `mdkg:hasRecallingManufacturer` and, for quoted barcodes, `mdkg:mentionsDeviceIdentifier`.

**Joining with other OKN graphs.** Addresses carry `mdkg:postalCode` (ZIP), `mdkg:city` and `mdkg:state`; establishments carry `mdkg:name` and WGS84 coordinates from the US Census geocoder. Product codes and manufacturers map to NAICS industries through `sudokn:hasNAICSClassifier` (an inferred crosswalk, labelled as such). These support joins by ZIP code with place-based graphs and by NAICS industry or firm name with manufacturing graphs.

**Remaining gaps.** FDA's Radiation Emitting Product Corrective Actions and Recalls search was unavailable (HTTP 503) throughout the build; a stand-in derived from recall data (recalls of radiation-emitting product codes, typed `mdkg:RadiationCorrectiveAction` and labelled as derived) is included. Device warning letters from May 2019 through 2020 are not available from FDA or its web archive.

**Responsible use.** MAUDE is passive surveillance: report counts are not failure rates, FDA does not verify causation, and the absence of reports is not evidence of safety. Alternative Summary Reports are summaries, not individual events, and can double-count with companion MAUDE reports.
