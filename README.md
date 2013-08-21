<a href="http://www.multicore-association.org/workgroup/tiwg.php" target="_blank"><img src="http://i.imgur.com/grXFUIT.png" title="Multicore Services Framework"/></a>

The ‘Multi-Core Services Framework’ (MCSF) specification defines a set of messages, data structures, interfaces and protocols that allow one or more "clients" to interact with services running on one or more "endpoints" on a heterogeneous multicore target device via a "heterogeneous network".  This GitHub repository stores an open-source reference implementation of the specification.


## Goals

* Provide access to services in the context of an arbitrary multi-core topology.   
* Provide facilities for efficient high bandwidth binary communications between clients and services on endpoints.
* Support communication between multiple clients and multiple endpoints concurrently
* Support communications over a heterogeneous network comprised of one or more physical communications links that connect the client and the endpoint via an arbitrary number of intermediary 'proxies'
* Provide a framework in which new services that target massive multi-core systems can be defined.
* Enable existing tools technologies (e.g. debuggers, tracers) to use MCSF as a transport for their existing services.  In doing this we enable existing technologies to scale to multi-core support incrementally and leverage a very large code base of existing tools.
* Provide layered standards and open source frameworks for those layers
* Highly scalable target endpoint code size.  From a dedicated single service running on a bare-metal DSP to a fully featured dynamically scaled agent running on Linux
* Provide BSD/MIT licensed open source implementations in both C and Java to encourage adoption by open source projects as well as MCA member companies
* Leverage and reuse existing technologies wherever it makes sense. We do NOT want to reinvent anything unnecessarily.

## About the Multicore Association (MCA)

For more information about the Multicore Association, please see <a href="http://www.multicore-association.org" target="_blank">http://www.multicore-association.org</a>

## About the MCA Tools Infrastructure Working Group (MCA TIWG)

For more information, please see <a href="http://www.multicore-association.org/workgroup/tiwg.php" target="_blank">http://www.multicore-association.org/workgroup/tiwg.php</a>