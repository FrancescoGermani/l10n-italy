=====================================
ITA - Fattura elettronica - Ricezione
=====================================

.. 
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! This file is generated by oca-gen-addon-readme !!
   !! changes will be overwritten.                   !!
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! source digest: sha256:d4ec3ab9daead49034699584170cf38181b935823c48710e5d7d844c6044c912
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

.. |badge1| image:: https://img.shields.io/badge/maturity-Beta-yellow.png
    :target: https://odoo-community.org/page/development-status
    :alt: Beta
.. |badge2| image:: https://img.shields.io/badge/licence-AGPL--3-blue.png
    :target: http://www.gnu.org/licenses/agpl-3.0-standalone.html
    :alt: License: AGPL-3
.. |badge3| image:: https://img.shields.io/badge/github-OCA%2Fl10n--italy-lightgray.png?logo=github
    :target: https://github.com/OCA/l10n-italy/tree/16.0/l10n_it_fatturapa_in
    :alt: OCA/l10n-italy
.. |badge4| image:: https://img.shields.io/badge/weblate-Translate%20me-F47D42.png
    :target: https://translation.odoo-community.org/projects/l10n-italy-16-0/l10n-italy-16-0-l10n_it_fatturapa_in
    :alt: Translate me on Weblate
.. |badge5| image:: https://img.shields.io/badge/runboat-Try%20me-875A7B.png
    :target: https://runboat.odoo-community.org/builds?repo=OCA/l10n-italy&target_branch=16.0
    :alt: Try me on Runboat

|badge1| |badge2| |badge3| |badge4| |badge5|

**Italiano**

Questo modulo consente di importare i file XML della fattura elettronica
versione 1.2

http://www.fatturapa.gov.it/export/fatturazione/it/normativa/f-2.htm

ricevuti attraverso il Sistema di Interscambio (SdI).

http://www.fatturapa.gov.it/export/fatturazione/it/sdi.htm

**English**

This module allows to import Electronic Bill XML files version 1.2

http://www.fatturapa.gov.it/export/fatturazione/en/normativa/f-2.htm

received through the Exchange System (ES).

http://www.fatturapa.gov.it/export/fatturazione/en/sdi.htm

**Table of contents**

.. contents::
   :local:

Installation
============

**Italiano**

Questo modulo richiede asn1crypto

https://github.com/wbond/asn1crypto

**English**

This module requires asn1crypto

https://github.com/wbond/asn1crypto

Configuration
=============

**Italiano**

Consultare anche il file README del modulo l10n_it_fatturapa.

Per ciascun fornitore è possibile impostare il "Livello dettaglio
e-fatture":

   -  Livello minimo: la fattura fornitore viene creata senza righe, che
      dovranno essere create dall'utente in base a quanto indicato nella
      fattura elettronica
   -  Livello massimo: le righe della fattura fornitore verranno
      generate a partire da tutte quelle presenti nella fattura
      elettronica

Nella scheda fornitore è inoltre possibile impostare il "Prodotto
predefinito per e-fattura": verrà usato, durante la generazione delle
fatture fornitore, quando non sono disponibili altri prodotti adeguati.
Il conto e l'imposta della riga fattura verranno impostati in base a
quelli configurati nel prodotto.

Tutti i codici prodotto usati dai fornitori possono essere impostati
nella relativa scheda, in

Magazzino → Prodotti

Se il fornitore specifica un codice noto nell'XML, questo verrà usato
dal sistema per recuperare il prodotto corretto da usare nella riga
fattura, impostando il conto e l'imposta collegati.

**English**

See also the README file of l10n_it_fatturapa module.

For every supplier, it is possible to set the 'E-bills Detail Level':

   -  Minimum level: Bill is created with no lines; User will have to
      create them, according to what specified in the electronic bill
   -  Maximum level: Every line contained in electronic bill will create
      a line in bill

Moreover, in supplier form you can set the 'E-bill Default Product':
this product will be used, during generation of bills, when no other
possible product is found. Tax and account of bill line will be set
according to what configured in the product.

Every product code used by suppliers can be set, in product form, in

Inventory → Products

If supplier specifies a known code in XML, the system will use it to
retrieve the correct product to be used in bill line, setting the
related tax and account.

Usage
=====

**Italiano**

   -  Andare in Contabilità → Acquisti → Fattura elettronica
   -  Caricare un file XML
   -  Visualizzare il contenuto della fattura facendo clic su "Mostra
      anteprima"
   -  Eseguire la procedura guidata "Importa e-fattura" per creare una
      fattura in bozza oppure "Collega a fattura esistente" per
      collegare il file XML a una fattura già (automaticamente) creata

Nell'elenco file delle fatture elettroniche in ingresso saranno
presenti, in modo predefinito, quelli da registrare. Sono i file che
devono ancora essere collegati a una o più fatture fornitore.

**English**

   -  Go to Accounting → Purchases → Electronic Bill
   -  Upload XML file
   -  View bill content clicking on 'Show preview'
   -  Run 'Import e-bill' wizard to create a draft bill or run 'Link to
      existing bill' to link the XML file to an already (automatically)
      created bill

In the incoming electronic bill files list you will see, by default,
files to be registered. These are files not yet linked to one or more
bills.

Known issues / Roadmap
======================

Il modulo contiene un cambiamento alla firma di un metodo in
``models/account.py`` il quale cambia da

``compute_xml_amount_untaxed(self, DatiRiepilogo)``

a

``compute_xml_amount_untaxed(self, FatturaBody)``

Il cambiamento è dovuto all'implementazione della gestione degli
arrotondamenti che posso essere presenti in 2 sezioni diverse del file
XML della fattura elettronica.

La soluzione ottimale è stata di cambiare la firma del metodo per
consentire la visibilità delle sezioni
``FatturaElettronicaBody.DatiBeniServizi.DatiRiepilogo`` e
``FatturaElettronicaBody.DatiGenerali.DatiGeneraliDocumento`` dove è
presente il nodo ``Arrotondamento``

Pertanto, al fine di ottenere il corretto valore del totale imponibile,
i moduli che avessero ridefinito il metodo
``compute_xml_amount_untaxed`` nel modello ``account.invoice`` dovranno
adeguare la chiamata al metodo stesso preoccupandosi di utilizzare come
primo parametro l'oggetto ``FatturaElettronicaBody``.

Bug Tracker
===========

Bugs are tracked on `GitHub Issues <https://github.com/OCA/l10n-italy/issues>`_.
In case of trouble, please check there if your issue has already been reported.
If you spotted it first, help us to smash it by providing a detailed and welcomed
`feedback <https://github.com/OCA/l10n-italy/issues/new?body=module:%20l10n_it_fatturapa_in%0Aversion:%2016.0%0A%0A**Steps%20to%20reproduce**%0A-%20...%0A%0A**Current%20behavior**%0A%0A**Expected%20behavior**>`_.

Do not contact contributors directly about support or help with technical issues.

Credits
=======

Authors
-------

* Agile Business Group
* Innoviu

Contributors
------------

-  Lorenzo Battistini <lorenzo.battistini@agilebg.com>
-  Roberto Onnis
-  Alessio Gerace
-  Sergio Zanchetta <https://github.com/primes2h>
-  Giovanni Serra <giovanni@gslab.it>
-  Gianmarco Conte <gconte@dinamicheaziendali.it>
-  Marco Colombo <https://github.com/TheMule71>
-  Salvo Rapisarda <https://github.com/salvorapi>

Maintainers
-----------

This module is maintained by the OCA.

.. image:: https://odoo-community.org/logo.png
   :alt: Odoo Community Association
   :target: https://odoo-community.org

OCA, or the Odoo Community Association, is a nonprofit organization whose
mission is to support the collaborative development of Odoo features and
promote its widespread use.

This module is part of the `OCA/l10n-italy <https://github.com/OCA/l10n-italy/tree/16.0/l10n_it_fatturapa_in>`_ project on GitHub.

You are welcome to contribute. To learn how please visit https://odoo-community.org/page/Contribute.
