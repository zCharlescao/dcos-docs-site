---
layout: layout.pug
navigationTitle:  Licenses
title: Licenses
menuWeight: 3
enterprise: true
---

Mesosphere uses licenses to ensure that customers respect their contract terms. The DC/OS licensing component tracks the state of a cluster license, collects information to check if any licensing terms have been breached, and supports operations for updating the license when a contract is extended or changed.

A cluster license file contains all of the information to determine if the terms of a contract agreement has been breached. It also contains the set of keys necessary to encrypt and decrypt auditing data gathered by the DC/OS licensing component. 


# Configuring the cluster license

You specify the license file as a base64 encoded string in the `config.yaml` file when you configure a cluster installation. The DC/OS licensing component will launch successfully only if the information in the license is legitimate. Once the DC/OS licensing component launches, the rest of the DC/OS components are started.

To configure a cluster license, specify the license text received in email sent by your Authorized Support Contact in the [`dcos_license`](/1.11/installing/custom/configuration/configuration_parameters/#dcos-license-enterprise-dcos-only) property of the `config.yaml` file. 


# License audit data

A license contains the maximum number of nodes attached to a cluster at any given time and the start and end date of the license.

Audit data about the number of nodes is gathered from the DC/OS metrics component every 30 min. Once a day, the DC/OS licensing component logs the number of nodes. The DC/OS licensing component also logs any graceful process shutdown. If the number of nodes exceeds the number specified in the contract, the DC/OS licensing component logs a breach of contract.

To validate that Mesosphere is not logging sensitive data you can retrieve the audit data decryption key through the API and CLI and decrypt the audit data checksum.