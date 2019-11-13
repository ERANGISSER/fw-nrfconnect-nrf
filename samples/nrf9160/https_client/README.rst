.. _https_client:

nRF9160: HTTPS client sample
############################

This HTTPS client sample is a minimal implementation of HTTP communication, showcasing how to
set up a TLS session towards a HTTPS server and sending an HTTP request.

Overview
********

The sample provisions a root CA certificate to the modem using :ref:`modem_key_mgmt`, after initializing ``bsdlib`` and AT communications.
Provisioning is done before connecting to the LTE network, since certificates can only be provisioned when the device is not connected.
The sample then connects to the LTE network, sets up the necessary TLS socket options, connectes to an HTTPS server and sends a HTTP HEAD request, printing the response code on the terminal.

Obtaining a certificate
***********************

The sample connects to ``www.google.com``, the required X.509 certificate is provided under :file:`samples/nrf9160/https_client/cert`.
To connect to other servers, a different certificate might need to be provisioned.
It is possible to download a certificate for a given server in using a web browser or dedicated web sites, for example `https://www.ssllabs.com/ssltest/`.
Certificates come in different formats; the one supported for provisioning to nRF9160 is the ``PEM`` format.
The ``PEM`` format looks like this:
```
"-----BEGIN CERTIFICATE-----\n"
"MIIDujCCAqKgAwIBAgILBAAAAAABD4Ym5g0wDQYJKoZIhvcNAQEFBQAwTDEgMB4G\n"
"A1UECxMXR2xvYmFsU2lnbiBSb290IENBIC0gUjIxEzARBgNVBAoTCkdsb2JhbFNp\n"
"Z24xEzARBgNVBAMTCkdsb2JhbFNpZ24wHhcNMDYxMjE1MDgwMDAwWhcNMjExMjE1\n"
"MDgwMDAwWjBMMSAwHgYDVQQLExdHbG9iYWxTaWduIFJvb3QgQ0EgLSBSMjETMBEG\n"
"A1UEChMKR2xvYmFsU2lnbjETMBEGA1UEAxMKR2xvYmFsU2lnbjCCASIwDQYJKoZI\n"
"hvcNAQEBBQADggEPADCCAQoCggEBAKbPJA6+Lm8omUVCxKs+IVSbC9N/hHD6ErPL\n"
"v4dfxn+G07IwXNb9rfF73OX4YJYJkhD10FPe+3t+c4isUoh7SqbKSaZeqKeMWhG8\n"
"eoLrvozps6yWJQeXSpkqBy+0Hne/ig+1AnwblrjFuTosvNYSuetZfeLQBoZfXklq\n"
"tTleiDTsvHgMCJiEbKjNS7SgfQx5TfC4LcshytVsW33hoCmEofnTlEnLJGKRILzd\n"
"C9XZzPnqJworc5HGnRusyMvo4KD0L5CLTfuwNhv2GXqF4G3yYROIXJ/gkwpRl4pa\n"
"zq+r1feqCapgvdzZX99yqWATXgAByUr6P6TqBwMhAo6CygPCm48CAwEAAaOBnDCB\n"
"mTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUwAwEB/zAdBgNVHQ4EFgQUm+IH\n"
"V2ccHsBqBt5ZtJot39wZhi4wNgYDVR0fBC8wLTAroCmgJ4YlaHR0cDovL2NybC5n\n"
"bG9iYWxzaWduLm5ldC9yb290LXIyLmNybDAfBgNVHSMEGDAWgBSb4gdXZxwewGoG\n"
"3lm0mi3f3BmGLjANBgkqhkiG9w0BAQUFAAOCAQEAmYFThxxol4aR7OBKuEQLq4Gs\n"
"J0/WwbgcQ3izDJr86iw8bmEbTUsp9Z8FHSbBuOmDAGJFtqkIk7mpM0sYmsL4h4hO\n"
"291xNBrBVNpGP+DTKqttVCL1OmLNIG+6KYnX3ZHu01yiPqFbQfXf5WRDLenVOavS\n"
"ot+3i9DAgBkcRcAtjOj4LaR0VknFBbVPFd5uRHg5h6h+u/N5GJG79G+dwfCMNYxd\n"
"AfvDbbnvRG15RjF+Cv6pgsH/76tuIMRQyV+dTZsXjAzlAcmgQWpzU/qlULRuJQ/7\n"
"TBj0/VLZjmmx6BEP3ojY+x1J96relc8geMJgEtslQIxq/H5COEBkEveegeGTLg==\n"
"-----END CERTIFICATE-----\n"
```
Note the "\n" at the end of each line.

A comprehensive tutorial on how to convert between certificate formats and encoding can be found at:
https://support.ssl.com/Knowledgebase/Article/View/19/0/der-vs-crt-vs-cer-vs-pem-certificates-and-how-to-convert-them


Requirements
************

* The following nRF device:

  * nRF9160

* .. include:: /includes/spm.txt


Building and running
********************

.. |sample path| replace:: :file:`samples/nrf9160/https_client`

.. include:: /includes/build_and_run.txt

The sample is built as a non-secure firmware image for the nrf9160_pca10090ns board.
Because of this, it automatically includes the :ref:`secure_partition_manager`.

Sample Output
=============

The sample displays the following:

.. code-block:: console

   HTTPS client sample started
   Provisioning certificate
   Waiting for network.. OK
   Connecting to google.com
   Sent 64 bytes
   Received 903 bytes

   >        HTTP/1.1 200 OK

   Finished, closing socket.

Dependencies
************

This sample uses the following libraries:

From |NCS|
  * ``lib/at_cmd``
  * ``lib/at_notif``
  * ``lib/modem_key_mgmt``
  * ``lib/lte_link_control``

From nrfxlib
  * :ref:`nrfxlib:bsdlib`

In addition, it uses the following samples:

From |NCS|
  * :ref:`secure_partition_manager`
