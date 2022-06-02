# Advist Exam 2022.04.20 [Theory]
## Intro Databases

### Biological Databases
#### Primary databases - repository for primary data with instututional funding
- DNA sequences (GenBank, ENA, DDBJ)
- Protein sequences (UniProtKB)
- Protein structures (PDB)

--> The Big Three:
- GenBank: DNA Sequences
    - annotaded collection of publicly available DNA sequences
- UniProtKB: Protein Sequences
    - collection of publicly available protein sequences 
    - Swiss-Prot: manually curated
    - TrEMBL: computationally analyzed
- PDB: Protein Structures
    - collection of three-dimensional structural data 

#### Secondary databases - manually curated topic related centric subsets that augument the primary data (project funding, sometimes outdated or out of maintenance)
- Structural hierarchies
    - Example: SCOP/CATH
        - organize the PDB protein structures
- Sequence families
    - Example: PFAM
        - database of protein families
- Specific organisms
    - Example: PROSITE
        - database of protein domains and functional sites

#### How to find databases?
- primary databases are already given. Google GenBank, UniProtKB and PDB
- secondary are more difficult sice there are much more of them: use website <b>Nucleic Acid Research</b>

## Genbank
Moved to NCBOI in 1992 <br>
NCBI - National Center for Biotechnology Information, part of US administration <br>
NCBI hosts following resources: <br>
- databases
- access as download
- submission portals
- documentations and howto's

GenBank - annotated collection of publicly available DNA sequences, has dialy synchronization with ENA and DDBJ. It is accessible online via Entrez Nucleotide, BLAST and NCBI e-utilites. Download via FTP in ASN.1 or flatfile format.

Represented species (from most bases to least): Human, Common Wheat, Fly, Durum Wheat, Barley, Rat, E.coli etc.

Genbank Flat file:
- fixed number of columns and variable number of rows (all rows have fixed layout)
- each entry starts with LOCUS record and ends with //
- Field Headers:
    - columns 1-10 contain fileed names, columns 13-80 field values
    - keywords start in column 1, subkeywords in column 3,4 
    - fileds can be mandatory or optional 
    - Filed may be limited to one line (record)
    - mandatory keywords: 
        - LOCUS: short mnemonic name of entry, chosen to suggest the sequence definition
        - ACCESSION: unique unchanging identifier assigned by and used for citation GenBank
        - DEFINITION: description of sequence
        - VERSION: identifier of the primary accession number and numeric version of the sequence
        - ORIGIN/SOURCE: common name of the organism or the name most freauently used in the literaturee
      
     - optional keywords: 
          - DBLINK: cross-references to resources that support the existence of a sequence record
          - KEYWORDS: short phrases describing the gene products and other information about entry (tags)
          
RefSeq : NCBI Reference Sequences: 
- explicitly linked nucleotide and protein sequences
- updates reflect curent knowledge of sequence data and biology 

Searching in NCBI --> Entrez:
- Entrez is a integrated web interface to access NCBI resources 
- provides API access 
E-Utilities:
- Einfo, Esearch, Epost, Esummary, Efethc, Elink, EGquery, Espell, ECitmatch
    - ESearch: input - text query (local search), return - list of matching UIDs in given database
    - ESumamry: input - list of UIDs from database, return - downoads document sumamries
    - EGQuery: input - text query (global search), return number of records matching the query in each Entrez database 
    - EInfo: database statistics
    - EFetch: input - list of UIDs in a given database, return - data records in a specified format
    - ELink: input - list of UIDs in a given database, return - list of related UIDs in same db or a list of linked UIDs in another Entrez db
    - EPost: input - (upload of UIDs)list of UIDs in a given database, return - query key and web environment for thee uplaoded dataset
    - ESpell: spelling suggestions for a text query in a given database
    - ECitMatch: input - set of citation strings, return - corresponding PubMed IDS
    
- Typical combination of queries:
    1. Get DocSumaaries: ESearch -> ESummary/EFetch, EPost -> ESummary/EFetch
    2. Filter record set: EPost/ELink -> ESearch

EDirect is a unix comand line front-end to the E-untilites 

## XML-WEB
### XML
#### General Information
XML(extensible markup language) - software and hardware independent tool to store and transport data. It is written in plain text.

XML tags are not predefined as HTML tags, so everybody can invesnt his own tags and new tags can be added ny time

The author of XML has to define content and structure of the document.

Elements are defined using tags: <tagName> ... </tagName> or <tagName/>

It is possible to have elements inside elements (nested) and they both can have text content. 

Mandatory is only one root element that is the parent of all other elements.
 
 ---
#### Syntax
tags are case sensitive and should be properly nested e.g. <a><b> .. </b></a>

tags may have attributes which should be quoted

Tag names:
- case sensitive
- start with letter or underscore
- cannot contain spaces

XML element:
- everything between start and end of a tag (tags are included)
- can contain: text, attributes, other elements, mix of all
- are extensible

XML attributes:
- values must be quoted with "" or ''
- cannot contain multiple values, be a tree structure and are in general not easy to extend
- you can store e.g. XML element id inside etc.
- to avoid name collisions prefixes are implemented:
    - xmlns: prefix = 'URI' --> <prefix:tagName>
    - URI is unique, tagName can have duplicates

How to understand than XML is correct?
--> it should contain:
- root element
- closing tag
- case sensitive
- proper nesting
- quotation of attribute values

Document type definitions:
- DTD
- XML Schema

#### XML DTD
referenced from a document with <!DOCTYPE note SYSTEM "Note.dtd">
- !DOCTYPE defines the root element
- !ELEMENT defines the structure of the elements
- #PCDTA means parse-able text data
- !ENTITY defines special characters of strings

#### XML with Python
import xml.etree.ElementTree as ET
- use defusedxml if working with XML from untrusted sources

- Read XML from file: parse('fileName')
- Read from string to tree element: fromString(data_as_string)
- Retrieve element from tree element: getroot()
- e.keys() - element attribtues
- access children xml element via index notation
- add element via writing into the file

## Web Access
### General information:
- URI (uniform resource identifier) --> string
- URL is specific URI with inlcusion of the location of the resource

scheme://location/path?query#fragment
https://www.rostlab.org/research/projects/protein-flexibility
- scheme: protocol in use e.g. HTTPS
- location: hosting server
- path: path to resource 
- query + fragment: optional specifications
### Web Acess with Python
from urllib import parse as urlparse
import requests 
- Request: models a HTTP request to the server
- Response: models the HTTP response
    - .status code: tells about success or failure
    - .content: content of response
    - .iter_lines chunkwise reading of reponse data
    
- Session: if you need continuity

## SwissProt
set of manually curated annotated protein sequences

subsection of UniProtKB

UniProKB:
- UniProtKB/Swiss-Prot
- UniProtKB/TrEMBL (automatically translated from the EMBL nucleotide database)

UniParc: pure sequence archive, no annotations

UniRef: consists of several databases of clustered sets of protein sequences (UniRef90..)

Proteomes: sets of proteoms

Integration of UniProtKB:
- hosted and maintained within ExPASy
- SIB Portal provides access to databases and tools

Top 10 represented species:
- Homo sapiens
- Mouse
- Nouse-ear cress
- Rat
... 

Swiss-Prot entries per taxonomic group:
1. Bacteria ~ 60%
2. Eukaryota ~ 30%
3. Arcaea + Viruses ~ 10%

Most common aminoacids:
- Leucine 9.6%
- Alanine 8.2%
- Glycine 7.0% 
--> all aliphatic

Least common aminoacids:
- Tryptophan 1.0%
- Cysteine 1.3%
- Histidine 2.2 %
--> Sulfur, Basic and Aromatic

### Annotation Phases
1. sequence curation
    - >95% translated from International Nucleotide Sequence Database Collaboration (INSDC)
    - sequnces are selected acc to the curation priorities
    - result is canonical sequence for a gene/species pair
        - for that: entries are selected
        - BLAST is runned to identify additional sequences of same gene or homologues 
2. sequence analysis
    - some analysis programs are applied to sequences to identify:
        - topological features
        - domains
        - post-translational modifications
    - results are manually checked and in or excluded for annotation
3. literature curation
    - identification of releveant scientific literature from PubMed, iHOP etc.
    - some information is extracted for annotations
        - e.g functions, pathway, cofactor, catalytic activity etc.
        - sequence annotations: regions, sites, aa modifications, secondary strucuture
4. family-base curation
    - evaluation of homologs
    - annotation of homologs
    - propagation of annotation across the homologs to ensure consistency
5. Evidence attribution
    - attribution of annotation to its original source
    - annotations are traced back and evaluated
    - GO term annotation
    - evidence distinction with ECO
6. quality assurance, integration and update
    - finished entries are run through a series of rule-based checks concerning especially positions and regions
    - correction of errors
    - reviewed by senior curator
    - intergration into the database
### Swiss-Prot flat file:
follows EMBL Nucleotide Sequence Database format as close as possible

2 sections:
- core data (sequence data, citation info, taxonomy)
- annotations (function, modification, domains, disease assosiation etc.)

table looks like this:

Header: Line Code, Content, Occuence per Entry

Line Code:
- ID, AC (accession nr), DT (date), DE (desc.), GN (gene name), OS (organism), OG (organelle), OC (organism classification), OX (taxonomy cross-ref), OH (organism host), KW (key words), FY (feature table data), SQ (sequence header), blanks (sequence), // (termination line)

### Programmatic access
https://www.uniprot.org/help/programmatic_access

Website REST API

## PDB
In general Protein 3d structure db:
- determine protein structures
- visualize structures

### How do you obtain protein 3d strcucture?
-> X-ray crystallography:
- measurement shows the electron density 
- the more resolution e.g 3.0 A the better the quality (1 A is still ok)

-> Electron Microscopy:
- measurement of electron diffraction and electron tomography
- reconstruction of electron density

### PDB compositions
- founded in 1968
- by far most of compositions are from  proteins and x-ray diffraction method
- second is NMR, third Electron microscopy

### PDB online
RSCB

PDBe

PDBj

### PDB file
- Header:
    - protein information
    - citation 
    - details about structure resolution
- Coordinates/Connectivity

Records in defined order and each lne is 80 chars wise
- col 1-6: record name
- col 7 blank

Some mandatory record types:
- header
- title
- compnd
- source
- keywds
- expdta

Sections (each section has multiple record types):
- title (summary descriptive marks)
    - record types: header, obslte, titlem ketwds etc
- remark (comments about entry annotations in more depth)
    - record types: remarks
- primary structure
- secondary strucutre:
    -  record types: helix, sheet
- connectivity annotation (chemical connectivity)
- and much more such as crystallographic, coordinate, bookkeeping etc.

#### PDB record format
- is individually defined per record type
- may have substructure

#### Parsing PDB files
use PDBParser from Bio Python Bio.PDB

### STAR
STAR file is a new format for electronic data transfer and archiving.

Advantages:
- extensible
- flexible with respect to order
- few syntax rules
- automatic validation possible with mmCIF

#### STAR syntax
- data name: any text string starting with underline e.g. _chemical_formula
- data item: any text string not starting with underline e.g. C23
- data loop: list of data names, preceded by 'loop_', followed by repeated data items
- data block: collection of data preceded by 'data_xxx'

#### Parsing mmCIF files with Python 
use modules:
- PDBx
- PDBeCIF
- mmLIB
- bioPython

### Molecular Graphics Programs
- PyMol
- Jmol
- Chimera
- VMD
- Yasara

## Secondary databases
= databases provides processed and structured data from primary systems
- Not always "true" dbs
- SCOP/CATH
- PFAM
- STRING
- PROSITE

### SCOP and CATH-Gene3D
= classificaiton of structures
- similar
- aim: arganize protein structures available in PDB based on single domains
- hierarchical system of SCOP:
    - secondary structure content
    - fold (shape of domain)
    - super families (least distanc common ancestor)
    - protein domains (same protein, isoform)
    - species 
- SCOP is fully manually curated by expert analysis

CATH:
- semi automatic procedure for deriving a novel hierarchical classification of protein domain structures
- four levels:
    - C: protein class, mainly secondary structure composition of each domain
    - A: architecture, summarizes shapes based on orientation of secondary strucutre elements
    - T: topology, sequenctial connectivity is considered
    - H: homologous superfamily, high similarity with similar functions, evolutionary relationship assumed

### PFAM
- protein families database hosted by EBI (based on sources from UniProtKB)
- Pfam-A: curated seed alignment derived from Pfamseq, profile HMMs for the seed alignment, full alignment with all HMM detected sequences
- Pfam-B: un-annotated, automatically generated from non-redundant cluster from ADDA
    - focuses on single domains
    
    
Family: collection of related protein regions <br>
Domain: structural unit <br>
Repeat: short unit which is unstable in isolation but forms stable structure when found in multiple copies <br>
Motif: short unit found outside of globular domains <br>
Clans: related group of Pfam entries based on similarity in sequence, structure of profile-HMM

### STRING
= database of known and predicted protein-protein interactions. 

Interactions inlcude physical and functional assosiations. They come from comp. prediction, knowledge transfer between organisms and from interactions aggregated from other primary databases.

### PROSITE
= contains of entries descibing protein domains, families and functional sites. It contains associated patterns and profiles too.

### ENCODE/UCSC Genome Browser
= integrated encyclopedia of DNA elements in the Human Genome
- founded by NHGRI (National Human Genome Research Institute)
- build a comprehensive parts of functional element in the human genome
- has elements that act on protein and RNA level and regulatory elements

## NoSQL

### SQL
- fixed schema
- typed data
- tables
- defined layout
- space consumption is computable
- relational algebra
- ACID principle 
    - atomicity, consistency, isolation, durability
- standardized query language
- fast access using indices
- well supported by software vendors

<b> Issues with relational dbs </b>
- if schema is bad, the query also is
- based on strings, susceptible for typos
- errors are not detected at compile time
- cannot be refactored (too expensive)

### NoSQL
- map/reduce
- bigtable databases
- data volume in the range of TB or PB
- non relational data model
- enables distribution and horizontal scalability
- open source
- simple schema or no at all
- simple data replication
- simple api

#### Categories of NoSQL
- key/value stores
- documents stores
- graph dbs
- columns familiy systems

#### Key/value systems
- key and value schema
- keys can be grouped in namespaces and dbs
- values can be strings or smth more complex e.g. hashes, sets and lists
#### Column Family
- keys can point to an arbitrary number of key/value pairs
- nested key/value pairs
- nested columns
#### Document stores
- works on structured data like JSON, YAML, RDF
#### Graph databases
- based on graph or tree structures to connect elements
- property graph: nodes to reflect items/entities, edges reflect to relations
- very suitable for traversing

### Theoretical concepts:
#### Map/Reduce:
- designed to efficient handling of data in the order of Tera or Peta bytes
- framework was developed by google
- MapReduce facilitates concurrent processing by splitting petabytes of data into smaller chunks, and processing them in parallel on Hadoop commodity servers. 
- map function: 
    - works in parallel and is applied to all elements of a list
    - returns a modified list
- reduce:
    - takes output of map() and returns values from Map into one result
    
#### CAP
- horizontal scaling of relational databases is not efficient
- CAP: 
    - 1. consistency - alle replicating nodes of dbs have the same state after a transaction, changes are immediatly propagated to all nodes. Read access to any node returns the same result.
    - 2. availability - acceptable response time, a certain response time is guaranteed up to a specific load level
    - 3. partition tolerance - if a node or part of a node fails the remaining nodes/data is still accessible
- cannot be satisfied at one time only CA, CP, AP

#### BASE Consistency model
- basically available
- soft state
- eventually consistent

focus on availability and consistency is less important. BASE defines consistency as a transition process and not as a defined state after transaction

#### MVCC
= multiversion concurrency control
- data object are versioned
- represents the change timeline
- every write access creates a new version
- conflict resolution through explicit version comparison

Disadvantages of a Conventional Lock?
- complete tables are locked
- not 100% guaranteed in distributed systems
- parallel access is blocked

Challenge:
- many instances write data
- they have to be synchronized and ordered afterwards
Solution: Vector Clocks
- weak consistency criterion: if event e1 causes e2 -> timestamp(e1) < timestamp(e2)
- strong consistency criterion: if timestamp(e1) < timestamp(e2) -> e1 is cause of e2
- version vector tuple of values/timestamps of an object
- vector clock: each database has a counter which is incremented
- every process remembers the sender and the timestamp
- every message has a vector of id-timestamp pairs attached

#### Vector Clocks in NoSQL:
- a list of ID x Time tuples
- enables the client ot sort and figure out the different versions of multiple clients update and replicate records at the same time.
- Example: What do 3 friends (L,P,A) want to do on Sunday:
    - L suggests jogging (message is sent to P and A)
    - P suggests surfing (message is sent to L and A)
        - message successuly delivered to L but not to A
    - L agrees with surfing (message is sent to P)
    - A agrees with jogging (delay) (message is sent to P)
    - P has a conflict. There are 2 possibilities to solve:
        - jogging bcs initially both L and A wanted to
        - surfing bcs Laura changed her mind
    - P decides to go on with surfing and communicates this to A and L
--> this is how vector clocks help to make decisions

### Graph Databases
with graphs we can represent connected information very intuitively by using vertices and edges e.g. internet routing, social network contacts, recommender systems, regulatory networks, semantic web
- specific APis vary heavily
- most of graph dbs support REST
- architecture for web apps
- implemented using http protocol
- set of access functions: POST (create), GET(read), PUT(udpate), DELETE(delete)

GET/HEAD:
- safe and idempotent (operations applied multiple times without changing the result beyond the initial application)
- HEAD: returns only meta data about the resource
- GET: contains in addition to meta data a representation of the resource
- GET: needs to include the querries into the URI

PUT:
- idempotent
- referenced resource reporesentation is transmitted to server
- only first execution changes the state of the server
- this can be achieved if server maintains version numbers for a document which has to be match by the request

DELETE:
- idempotent: once the resource is removed all subsequent requests fail (server state remains the same)
- referred resource is removed from the server/access blocked

POST:
- not guarantees  at all
- transmits data for processing
- processing result can be used to create new resource, modify esisitng one or not at all
- include the querries into the body of request. -> can be used for more complex 

### Document stores
- responsibility for the schema is moved from the database towards the application
    - loss of enfocement of normalization and referenial integrity
    - gain of flexibility and schema modifications at run-time
    
- data is stored as JSON

### MongoDB
- document store
- tries to close the gap between RDBMS and key/value stores
- Database: container for collections
- Collection: a group of MongoDB documents e.q. to a table
    - typically similar structured documents but no enforce schema
- Document: set of key/value pairs, value can be a list or nested document
- design: acc to your requirements
- joins are not supported, but you can combine objects int one document

JSON in MongoDB:
- each document needs a special ID field: _id

Commands:
- select database: _use database_name_
- check your database: _db_
- show available dbs: _show dbs_
- drop dbs: _db.dropDatabase()_
- create collection: _db.createCollection(name, options)_:
    - options: key:value style, autoindexing, size limit etc.
- drop collection: _db.collection_name.drop()_
- insert document: _db.collection_name..insert(documents[s])_ (list of documents in array style []). Id is autogenerated by db (if not given).
- find documents: _db.collection_name.find({criteria}, {fields_to_show})
    - e.g. print whole collection: _db.mycol.find({},{"title":1, _id:0}
- update: _db.collection_name.update({criteria}, {updated_data}
    - e.g. _db.mycol.update({'title': 'MongoDB Overview'}, {$set:{'title':'New MongoDB Tutorial'}})
    
## Graph DB

Graphs allow to represent connected information very inuitively by using vertices and edges<br>
The graph based databases are commonly used in:
- internet routing
- contacts in social networks
- recommender systems
- fraud detection
- regulatory networks
- semantic web
- all kinds of interaction

Graphs are represented by a pair of two sets V and E. V-vertices are nodes representing a kind of fact/evidence/entity. E-edges are connections between the vertices and represent relationships. Graphs can be directed or undirected.<br>
G = (V,E), V = {1,2}, E = V x V = {(1,2)}

### Property graph model
directed, multi-relational graph

labeled/typed edges

both vertices and label have properties

Properties are key/value pairs of type <String, Object> e.g. Age:30, Name:Bob

bidirectional edges are realized by two unidirectional edges

multi-edges require different labels

### Model Extensions
higher order relations with hyper edges and hyper nodes:
- hyper edge: connect more than two nodes
- hyper vertix: combination of a set of vertices/nodes, keeps intenal edges

Paths: sequence of edges

Subgraphs: defined combination of nodes and edges into a single node

Version information allows to represent the graph evolution and/or concurrency. 

### Graph Representations
#### Adjacency matrix
- square matrix/table
- all n nodes are listed horizontally and vertically 
- if an edge exists between u and v there is an entry in the table at position [u,v]
- test for the connection between the two nodes v and u can be done very quick
Problems:
- huge space consumption 
- difficult to identify all the connection edges for a given node
- neighbours identification is unefficient 
- hypergaphs can not be represented

#### Incidency matrix
- matrix with nodes on one axis and edges on the other axis
- e.g. we have a bidirectional node e10 from node v1 and v3 then: matrix[e10][v1] = 1 and matrix[e10][v3] = 1
- if one directional node e20 from v1 to v3 then: matrix[e10][v1] = 1 and matrix[e10][v3] = -1
Advantages:
- more space efficient (especiallky for weakly connected graphs)
- can represent hypergraphs
Problems:
- can be less space efficient if graphs are more connected than adjacency matrix

#### Edge List
- nodes and edges are stored separatly
- insertion and deletion of a single edge is efficient
- identification of connected edges given a node is inefficient

#### Adjacency List
- extention of edge list
- edges are sorted according to their start node
- for every node the connecting edges are stored

### Graph traversal
- breadth-first/depth-first
- algorithmic traversals
- random based

### Graph query languages
no common standard yet
- pattern based: SPARWL, RDF Query language, Cypher
- navigation based: Gremlin, sonesGQL
- login-based: OWL, GraphLog

#### Apache Tinkerpop
- attempt to provide uniform interfaces for property-graph based systems
- separates the backend database from the application developer
-supports Gremlin query language with many dialects

#### Gremlin Shell
- uses Groovy
- used to describe graph traversals (moving over the graph elements in a configurable way)

Short overview:
Essential components of a graph:
- data structure that stores the informatiom
- traversal/query engine
- language to express the queries (like Gremlin and Cypher)

Gremlin query:
- graph object
- traversal object
- chain steps over vertices and edges to navigate the graph
- steps may contain predicates over labels or properties

Neo4J:
- standalone graph database, embedded or as server
- support for ACID
- can be connected to Gremlin
- uses Cypher query language

Cypher:
- declarativd language 
- allows to specify labels and properties in the query by variable bining
- typical structure:
    - match, where, return(sort, limit)