---
title: Hvordan komme i gang
description: Hvordan registrere sluttbrukersystem / SFTP-bruker og etablere system id
weight: 900
---

{{< figure src="/docs/images/guides/sluttbrukersystemer/hvordan-komme-i-gang.png" title="">}}

Registrere sluttbrukersystem / etablere system id
-------------------------------------------------

Eieren av et sluttbrukersystem må registrere dette i Altinn slik at Altinn har mulighet til å autentisere og autorisere systemet på vegne av en avgiver. Ved registrering i portalen opprettes en unik sluttbrukersystemidentifikator, og denne identifikatoren sendes med i alle web service kall som gjøres mot Altinn. Sluttbrukersystemet har da rett til å levere data for alle avgivere eieren av sluttbrukersystemet har rett til å levere for. Eierens rettigheter hentes i utgangspunktet fra enhetsregisteret, men det er også mulig for en avgiver å legge på disse rettighetene eksplisitt i portalen. For å unngå ekstra administrasjon er det derfor meget viktig at avgivere sørger for at enhetsregisteret til enhver tid er oppdatert med korrekte opplysninger.

For at et sluttbrukersystem skal kunne gi data til skjema i Altinn, må den ansvarlige for selskapet, for eksempel daglig leder eller styreformann registrere systemet i Altinn portal. Dette gjøres fra siden
Brukeradministrasjon på følgende måte:

Alternativt kan en bruker også benytte sitt registrerte brukernavn til å bruke tjenestene beskrevet.

Det er da brukerens profil-brukernavn og passord som benyttes i stedet for sluttbrukersystem. Dette gjøres ved å gå inn på «Min Profil» og huke av under «Tillat innsending fra applikasjon eller system med dette brukernavn og passord» i Innloggingsinformasjon. Denne brukeren har kun rettighet til å levere data på vegne av seg selv.

For videre informasjon om registrering og rettighetsadministrasjon, benytt hjelpesystemet til Altinn på
[*http://www.Altinn.no*](http://www.altinn.no/).

Registrere SFTP-bruker
----------------------

For å kunne benytte seg av formidlingstjenester over SFTP-kanalen må det opprettes en virksomhetsbruker med et eget sertifikat. En slik bruker benytter seg av, i tillegg til brukernavn og passord, et sertifikat for å autentisere seg mot Altinns SFTP-server. Når bruker opprettes i Altinns profilsider lastes offentlig nøkkel opp og knyttes til virksomhetsbrukeren, og når denne brukeren så skal autentisere seg mot SFTP-serveren oppgis den private nøkkelen. Sertifikatet, eller nøkkelparet, kan genereres av bruker selv, for eksempel ved bruk av tilgjengelig verktøy slik som PuttyGen[^2]. Formatet som skal benytteser enten OpenSSH eller SSH2.

Merk at virksomhetsbrukere også kan ha et signert sertifikat, for eksempel BuyPass eller Commfides, knyttet til seg. Disse typene sertifikater gir brukeren tilgang til web service og portal, men ikke SFTP.

For at en SFTP-bruker skal kunne benytte en formidlingstjeneste må nødvendige rettigheter være delegert til virksomhetsbrukeren. Dette gjøres på normal måte.

Kovertering fra x.509 sertifikater til SSH2
----------------

For å konvertere et x.509 sertifikat til SSH2 format, som er mulig å bruke for formidlingstjenestens SFTP må man generere en public key i SSH2 format. Dette kan gjøres i verktøyet PuttyGen ved å følge punktene under.

- Eksporter private key fra x.509 sertifikatet.
- Pass på at PuttyGen her satt i SSH2 format, og ikke SSH1
- Importer private key inn i puttygen, dette genererer automatisk en public key basert på private key.
- Lagre public key fra PuttyGen, denne er nå i SSH2 format, og kan brukes i Altinn.
- Hvis ønskelig kan private key nå også lagres fra PuttyGen, og denne vil da også være i SSH2 format.

Etter at man har generert opp nøkkel i SSH2 format, og koblet denne på en bruker i Altinn, så kan man enten bruke det originale x.509 sertifikatet for oppkobling fra SFTP klient, eller benytte seg av eventuelt ny lagret private key i SSH2 format