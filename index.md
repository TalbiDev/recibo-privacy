---
title: Privacy Policy — Recibo
---

# Privacy Policy — Recibo

Last updated: 2026-11-11

This policy describes how the Android app **Recibo** (receipt-based expense tracking), developed by T.Dev, handles your data. *Une version française suit la version anglaise.*

In short: Recibo works fully offline without an account. An account (Sign in with Google) is optional and only needed to scan receipts automatically and to back up and sync your data to the cloud. When your monthly scans run out, you can choose to watch a video ad to get bonus scans: this optional feature uses Google AdMob, which collects data under Google's own terms (section 10). Apart from AdMob and the diagnostic data described in section 3, Recibo integrates no advertising or analytics SDK. We do not sell your data.

**Data controller:** Said Talbi (T.Dev). Contact: [talbidev@gmail.com](mailto:talbidev@gmail.com)

## 1. Data we collect

**Without an account**, everything you enter stays on your device: receipts (amount, currency, merchant, category, day, payment method, note, photo), budgets, categories, merchant classification rules and settings. Nothing is sent to us. Automatic scanning and video ads are not available without an account; manual entry remains fully available.

**With an account**, we process:

- **Account data, received from Google when you sign in** and stored by our authentication service (Supabase Auth): your email address, your full name, the URL of your profile photo and your Google account identifier, together with a unique Recibo account identifier.
- **Synced data:** your receipts (day, total amount, tax amount, currency, payment method, merchant, category, note, processing status, extraction confidence scores and suggested category), merchants, merchant classification rules, custom categories and budgets, together with creation, modification and deletion dates.
- **Receipt photos**, uploaded to private cloud storage as part of sync.
- **Scan usage:** a monthly counter of the number of automatic scans used by your account (a limited monthly allowance shown in the app).
- **Bonus scans from videos:** for each month, the number of bonus scans granted and used, and the number of videos watched on the current day; and, for each video, a record of the reward: a random one-time code issued by our service, the time it was issued and credited, the number of bonus scans credited and the transaction identifier sent by Google to confirm the reward.
- **Receipts sent for scanning:** when you scan or import a receipt, its image is sent to our extraction service to read the amount, merchant, date and so on (see section 3). Capturing and cropping the receipt happen on your device; only the receipt image is sent.
- **Technical logs of the extraction service:** time of the request, a truncated IP address (last part of an IPv4 address, last half of an IPv6 address masked), request size, response status, response time, a short irreversible fingerprint of your account identifier, the outcome of access checks (identity check, refusal reason, rate-limit decision), for bonus-scan requests the outcome and short irreversible fingerprints of the one-time code and of Google's transaction identifier, and technical error events of the scan counter or of the AI service (event name, error cause, status code). These logs never contain the image, the extracted data, your email address, your account identifier in clear, or the one-time code and transaction identifier in clear.

**Data collected by Google when you use video ads** is described in section 10.

**Data that stays on your device only, even with an account:** your preferences (display currency, language, scan reminder, onboarding state), the home-screen widget's state, budget alert history, and the state of financial advice cards.

## 2. Why we use it

- To provide the app: store, display and compute your expenses (all totals and statistics are calculated on your device).
- To read receipts automatically when you scan them.
- To back up your data and sync it between your devices when you are signed in.
- To enforce the monthly scan allowance and protect the service from abuse (rate limiting).
- To grant bonus scans after a video and make sure each video is credited only once.
- To diagnose errors in the extraction service.

**Legal bases:** performance of the service you request (account, sync, receipt reading, scan allowance, bonus scans); legitimate interest (abuse prevention, rate limiting, technical logs, diagnostics); your consent, where the law requires it, for video ads (section 10).

We do not use your data for advertising or profiling, or to train AI models, and we do not sell it. Google's use of the data its advertising SDK collects is described in section 10.

## 3. Storage and service providers

- **Supabase** (database, authentication, file storage) hosts your account, your synced data, your receipt photos, your scan counter and your bonus-scan records. The production project is hosted in the eu-central-1 region (Frankfurt, European Union). Data is encrypted in transit (TLS) and at rest (AES-256). Currently, our database has no managed backups: when your account is deleted, the deletion is final immediately. Privacy policy: <https://supabase.com/privacy>
- **Cloudflare** (Workers) runs the extraction service that receives a receipt image, forwards it for reading and returns the result. The image is not stored. The same service issues the one-time code for a video and receives Google's confirmation of the reward. Its technical logs (section 1) are kept for up to 7 days. Privacy policy: <https://www.cloudflare.com/privacypolicy/>
- **Anthropic** (Claude API) reads the receipt image and returns the extracted fields. Only the image and a fixed instruction are sent: no account identifier, email address or other data. Anthropic does not use this data to train its models and deletes it within 30 days, unless it must be kept to comply with the law or because it was flagged for abuse. Privacy policy: <https://www.anthropic.com/legal/privacy>
- **Google** provides Sign in with Google (through Android's Credential Manager) and the on-device document scanner (ML Kit, Google Play services) used to capture receipts. The scanner captures and crops the receipt on your device; the resulting image is then handled by Recibo as described above. During a scan, Google Play services (ML Kit Document Scanner) may collect diagnostic information and device identifiers (device model, operating system version, performance, error codes), under Google's privacy policy. Google also provides the video ads (AdMob) and the consent form (User Messaging Platform) described in section 10; for these, Google does not act on Recibo's behalf. Privacy policy: <https://policies.google.com/privacy>
- **Android backup** (Google): if you have Android backup turned on, Recibo's local database and settings may be included in your device backup (see section 6).

## 4. International transfers

Your account, synced data, receipt photos and bonus-scan records are hosted by Supabase in the European Union (Frankfurt). Cloudflare (global network), Anthropic (United States) and Google, including for video ads, may process data outside your country, under their respective data processing terms.

## 5. Retention

- **On your device:** until you delete it in the app, erase the app's data or uninstall the app.
- **In the cloud:** for as long as your account exists. A receipt you delete permanently has its photo removed from cloud storage; a minimal record of the deletion is kept so that your other devices also remove it, until your account is deleted.
- **Scan counter:** one row per month, kept until your account is deleted.
- **Bonus scans and video records:** kept for as long as your account exists and deleted with it. Bonus scans can only be used during the month they were credited.
- **Extraction service logs:** kept for up to 7 days.
- **Receipt images sent for scanning:** not stored by our extraction service; deleted by Anthropic within 30 days (see section 3).
- **Data collected by Google for video ads:** kept by Google under its own policies (section 10).
- **Backups:** currently, our database has no managed backups, so no copy of your cloud data remains in a backup after your account is deleted.

## 6. Security

- All traffic between the app and our services uses encrypted connections (HTTPS, TLS). The Supabase database and file storage are encrypted at rest (AES-256).
- Access rules in the database (row-level security) ensure that each account can only read and write its own data. Receipt photos are stored in a private bucket, never reachable by a public link. Bonus-scan records cannot be read or written by the app directly: only our extraction service handles them.
- A bonus scan is credited only after our service has verified Google's signed confirmation of the reward; what the app reports is never trusted on its own.
- On your device, receipt photos are stored in the app's private storage, never in your public gallery.
- Android cloud backup is limited to Recibo's database and settings, and only when the backup can be end-to-end encrypted (a screen lock is set); receipt photos and sign-in tokens are excluded. On Android 8.0 and 8.1, backup is turned off.
- The app contains no API key for the AI service: it is held only by our extraction service.

## 7. Your rights

Depending on where you live, you have the right to:

- **Access and portability:** all your data is visible in the app, and you can export your receipts as a CSV file (Receipts → Export → Export as CSV, which exports the current, filtered list; or select receipts → Export → Export as CSV). Photos are not included in the export.
- **Rectification:** edit any receipt, category, merchant or budget in the app.
- **Deletion:** delete individual items in the app. A deleted receipt (Delete on the receipt, or select receipts → Move to trash) goes to the trash (Settings → Trash), where you can restore it for 30 days; after that, it is permanently deleted, with its photo, the next time the app is opened. From the trash, Delete permanently erases it right away. You can also delete your account, in the app or on the web (section 8).
- **Objection and restriction:** you can stop all cloud processing at any time by signing out or deleting your account; the app keeps working locally.
- **Withdrawing consent to ads:** see section 10.

For any request, contact us (section 12). You may also lodge a complaint with your local data protection authority.

## 8. Deleting your account

- **In the app:** Settings → Delete my account (visible when signed in). You will be asked to sign in with Google again to confirm.
- **Without the app:** follow the instructions at <https://talbidev.github.io/recibo-delete-account/>.

Deleting your account permanently and immediately removes your account, all your synced data, your receipt photos stored in the cloud, your scan counter and your bonus-scan records (there is no backup from which they could be restored). The extraction service's technical logs (kept for up to 7 days) and the receipt images sent to Anthropic (kept for 30 days at most) expire on their own after the deletion, as described in section 5. Data collected by Google for video ads is not held by us and is not affected: see section 10. The data on your device is not touched: to remove it too, uninstall the app or clear its data in Android's system settings (Settings → Apps → Recibo → Storage → Clear data; the in-app entry Settings → Erase this device's data opens this screen).

## 9. Children

Recibo is not directed at children under 13, and we do not knowingly collect personal data from them.

## 10. Advertising: rewarded videos

**When videos are offered.** Only to signed-in users, and only when the monthly scans and the bonus scans are used up: in the message shown when a scan is refused for that reason, and in the menu used to add a receipt. Watching a video is optional and gives bonus scans. Videos are never shown during sync or exports, and never required to use the app: manual entry always remains available.

**Who processes the data.** Videos are provided by Google AdMob. Google is an independent third party that uses the data collected by its SDK for its own purposes (advertising, analytics, fraud prevention), under its own policies, and not on Recibo's behalf. When the app loads or shows a video, the Google Mobile Ads SDK collects, according to Google: your device's IP address (which may be used to estimate its approximate location), your interactions with the ad (such as app launch, taps and video views), diagnostic and performance information about the app and the SDK, and device identifiers (the Android advertising ID, the app set ID and, where applicable, other identifiers related to signed-in accounts on the device). A video may be loaded in advance, as soon as it can be offered, before you choose to watch it.

**What Recibo does not send to Google.** No account identifier, no email address and no receipt data. To credit the reward, Google sends our service a signed confirmation containing the random one-time code issued for that video and a transaction identifier (section 1).

**Consent.** In the European Economic Area, the United Kingdom and Switzerland, ads are shown only after you make a choice in Google's consent form, which opens when you first tap the video button. Without consent, no video is shown and manual entry remains available. You can review or withdraw your choice at any time in Settings → Ad privacy options (shown when this choice applies to you). Depending on your choices and your device's ad settings, Google may show personalized or non-personalized ads.

**Your controls.** You can reset or delete your advertising ID in Android's settings (Ads section, under Google or Privacy depending on the device). Google's own data, including how long it keeps it, is managed by Google: see how Google uses information from apps that use its services, <https://policies.google.com/technologies/partner-sites>, and Google's privacy policy, <https://policies.google.com/privacy>.

**Bonus scans.** Bonus scans can be used only during the month they were credited and are lost at the monthly reset. The number of bonus scans per video, the number of videos per day and the availability of videos may change at any time without notice. Bonus scans already credited remain usable until the monthly reset.

## 11. Changes to this policy and to the service

We may update this policy. Changes will be posted on this page with a new "Last updated" date.

There is no limit on cloud storage today. If a limit is ever introduced, it will be announced at least 30 days in advance, and data you already have will never be deleted because of it.

## 12. Contact

Questions or requests: [talbidev@gmail.com](mailto:talbidev@gmail.com)

---

# Politique de confidentialité (français)

Dernière mise à jour : 2026-11-11

Cette politique décrit la manière dont l'application Android **Recibo** (suivi de dépenses à partir de reçus), développée par T.Dev, traite vos données.

En bref : Recibo fonctionne entièrement hors ligne, sans compte. Un compte (connexion avec Google) est facultatif : il n'est nécessaire que pour scanner automatiquement les reçus et pour sauvegarder et synchroniser vos données dans le cloud. Quand vos scans du mois sont épuisés, vous pouvez choisir de regarder une vidéo publicitaire pour obtenir des scans bonus : cette fonction facultative utilise Google AdMob, qui collecte des données selon les conditions de Google (section 10). En dehors d'AdMob et des données de diagnostic décrites en section 3, Recibo n'intègre aucun SDK de publicité ni d'analyse. Nous ne vendons pas vos données.

**Responsable du traitement :** Said Talbi (T.Dev). Contact : [talbidev@gmail.com](mailto:talbidev@gmail.com)

## 1. Données collectées

**Sans compte**, tout ce que vous saisissez reste sur votre appareil : reçus (montant, devise, marchand, catégorie, jour, moyen de paiement, note, photo), budgets, catégories, règles de classement des marchands et réglages. Rien ne nous est envoyé. Le scan automatique et les vidéos publicitaires ne sont pas disponibles sans compte ; la saisie manuelle reste entièrement disponible.

**Avec un compte**, nous traitons :

- **Données du compte, reçues de Google à la connexion** et conservées par notre service d'authentification (Supabase Auth) : votre adresse e-mail, votre nom complet, l'URL de votre photo de profil et l'identifiant de votre compte Google, ainsi qu'un identifiant de compte Recibo unique.
- **Données synchronisées :** vos reçus (jour, montant total, montant de taxe, devise, moyen de paiement, marchand, catégorie, note, statut de traitement, indices de confiance de l'extraction et catégorie suggérée), marchands, règles de classement, catégories personnalisées et budgets, avec leurs dates de création, de modification et de suppression.
- **Photos des reçus**, envoyées dans un stockage cloud privé lors de la synchronisation.
- **Consommation de scans :** un compteur mensuel du nombre de scans automatiques utilisés par votre compte (un nombre limité de scans par mois, affiché dans l'app).
- **Scans bonus obtenus par vidéo :** pour chaque mois, le nombre de scans bonus accordés et utilisés, et le nombre de vidéos regardées le jour même ; et, pour chaque vidéo, une trace de la récompense : un code à usage unique tiré au hasard par notre service, l'heure de son émission et de son crédit, le nombre de scans bonus crédités et l'identifiant de transaction envoyé par Google pour confirmer la récompense.
- **Reçus envoyés au scan :** quand vous scannez ou importez un reçu, son image est envoyée à notre service d'extraction pour en lire le montant, le marchand, la date, etc. (voir section 3). La capture et le recadrage du reçu se font sur votre appareil ; seule l'image du reçu est envoyée.
- **Journaux techniques du service d'extraction :** heure de la requête, adresse IP tronquée (dernière partie d'une adresse IPv4, seconde moitié d'une adresse IPv6 masquées), taille de la requête, statut et durée de la réponse, une empreinte courte et irréversible de votre identifiant de compte, le résultat des contrôles d'accès (vérification de l'identité, motif d'un refus, décision de la limitation de débit), pour les requêtes de scans bonus le résultat et des empreintes courtes et irréversibles du code à usage unique et de l'identifiant de transaction de Google, et les événements d'erreur technique du compteur de scans ou du service d'IA (nom de l'événement, cause de l'erreur, code de statut). Ces journaux ne contiennent jamais l'image, les données extraites, votre adresse e-mail, votre identifiant de compte en clair, ni le code à usage unique et l'identifiant de transaction en clair.

**Les données collectées par Google quand vous utilisez les vidéos publicitaires** sont décrites en section 10.

**Données qui restent sur votre appareil, même avec un compte :** vos préférences (devise d'affichage, langue, rappel de scan, état de l'accueil), l'état du widget d'écran d'accueil, l'historique des alertes de budget et l'état des cartes de conseils.

## 2. Finalités

- Fournir l'application : enregistrer, afficher et calculer vos dépenses (tous les totaux et statistiques sont calculés sur votre appareil).
- Lire automatiquement les reçus que vous scannez.
- Sauvegarder vos données et les synchroniser entre vos appareils lorsque vous êtes connecté.
- Appliquer le quota mensuel de scans et protéger le service contre les abus (limitation de débit).
- Accorder les scans bonus après une vidéo et s'assurer que chaque vidéo n'est créditée qu'une fois.
- Diagnostiquer les erreurs du service d'extraction.

**Bases légales :** exécution du service que vous demandez (compte, synchronisation, lecture des reçus, quota de scans, scans bonus) ; intérêt légitime (prévention des abus, limitation de débit, journaux techniques, diagnostic) ; votre consentement, lorsque la loi l'exige, pour les vidéos publicitaires (section 10).

Nous n'utilisons pas vos données pour la publicité, le profilage ou l'entraînement de modèles d'IA, et nous ne les vendons pas. L'usage que Google fait des données collectées par son SDK publicitaire est décrit en section 10.

## 3. Stockage et sous-traitants

- **Supabase** (base de données, authentification, stockage de fichiers) héberge votre compte, vos données synchronisées, les photos de vos reçus, votre compteur de scans et vos traces de scans bonus. Le projet de production est hébergé dans la région eu-central-1 (Francfort, Union européenne). Les données sont chiffrées en transit (TLS) et au repos (AES-256). Actuellement, notre base de données n'a pas de sauvegarde gérée : quand votre compte est supprimé, la suppression est définitive immédiatement. Politique de confidentialité : <https://supabase.com/privacy>
- **Cloudflare** (Workers) exécute le service d'extraction, qui reçoit l'image d'un reçu, la transmet pour lecture et renvoie le résultat. L'image n'est pas conservée. Le même service émet le code à usage unique d'une vidéo et reçoit la confirmation de la récompense envoyée par Google. Ses journaux techniques (section 1) sont conservés jusqu'à 7 jours. Politique de confidentialité : <https://www.cloudflare.com/privacypolicy/>
- **Anthropic** (API Claude) lit l'image du reçu et renvoie les champs extraits. Seuls l'image et une consigne fixe sont envoyés : aucun identifiant de compte, aucune adresse e-mail, aucune autre donnée. Anthropic n'utilise pas ces données pour entraîner ses modèles et les supprime dans un délai de 30 jours, sauf obligation légale ou signalement d'abus. Politique de confidentialité : <https://www.anthropic.com/legal/privacy>
- **Google** fournit la connexion avec Google (via le Credential Manager d'Android) et le scanner de documents sur l'appareil (ML Kit, services Google Play) utilisé pour photographier les reçus. Le scanner capture et recadre le reçu sur votre appareil ; l'image obtenue est ensuite traitée par Recibo comme décrit ci-dessus. Pendant un scan, les services Google Play (ML Kit Document Scanner) peuvent collecter des informations de diagnostic et des identifiants d'appareil (modèle de l'appareil, version du système, performances, codes d'erreur), selon la politique de confidentialité de Google. Google fournit aussi les vidéos publicitaires (AdMob) et le formulaire de consentement (User Messaging Platform) décrits en section 10 ; pour ceux-ci, Google n'agit pas pour le compte de Recibo. Politique de confidentialité : <https://policies.google.com/privacy>
- **Sauvegarde Android** (Google) : si la sauvegarde Android est activée, la base locale et les réglages de Recibo peuvent faire partie de la sauvegarde de votre appareil (voir section 6).

## 4. Transferts internationaux

Votre compte, vos données synchronisées, les photos de vos reçus et vos traces de scans bonus sont hébergés par Supabase dans l'Union européenne (Francfort). Cloudflare (réseau mondial), Anthropic (États-Unis) et Google, y compris pour les vidéos publicitaires, peuvent traiter des données hors de votre pays, selon leurs conditions de traitement des données respectives.

## 5. Conservation

- **Sur votre appareil :** jusqu'à ce que vous les supprimiez dans l'application, effaciez les données de l'application ou la désinstalliez.
- **Dans le cloud :** tant que votre compte existe. Un reçu supprimé définitivement voit sa photo retirée du stockage cloud ; une trace minimale de la suppression est conservée, pour que vos autres appareils le suppriment aussi, jusqu'à la suppression de votre compte.
- **Compteur de scans :** une ligne par mois, conservée jusqu'à la suppression du compte.
- **Scans bonus et traces des vidéos :** conservés tant que votre compte existe et supprimés avec lui. Les scans bonus ne peuvent servir que pendant le mois où ils ont été crédités.
- **Journaux du service d'extraction :** conservés jusqu'à 7 jours.
- **Images envoyées au scan :** non conservées par notre service d'extraction ; supprimées par Anthropic dans un délai de 30 jours (voir la section 3).
- **Données collectées par Google pour les vidéos publicitaires :** conservées par Google selon ses propres règles (section 10).
- **Sauvegardes :** actuellement, notre base de données n'a pas de sauvegarde gérée ; aucune copie de vos données cloud ne subsiste donc dans une sauvegarde après la suppression de votre compte.

## 6. Sécurité

- Tous les échanges entre l'application et nos services passent par des connexions chiffrées (HTTPS, TLS). La base et le stockage de fichiers Supabase sont chiffrés au repos (AES-256).
- Des règles d'accès dans la base (sécurité au niveau des lignes, RLS) garantissent que chaque compte ne peut lire et écrire que ses propres données. Les photos des reçus sont stockées dans un espace privé, jamais accessible par un lien public. Les traces de scans bonus ne peuvent être ni lues ni écrites directement par l'application : seul notre service d'extraction y accède.
- Un scan bonus n'est crédité qu'après vérification par notre service de la confirmation signée de la récompense envoyée par Google ; ce que l'application déclare n'est jamais cru sur parole.
- Sur votre appareil, les photos des reçus sont stockées dans l'espace privé de l'application, jamais dans votre galerie publique.
- La sauvegarde cloud d'Android se limite à la base et aux réglages de Recibo, et seulement si elle peut être chiffrée de bout en bout (verrouillage d'écran configuré) ; les photos des reçus et les jetons de connexion en sont exclus. Sous Android 8.0 et 8.1, la sauvegarde est désactivée.
- L'application ne contient aucune clé d'API du service d'IA : seul notre service d'extraction la détient.

## 7. Vos droits

Selon votre lieu de résidence, vous disposez des droits suivants :

- **Accès et portabilité :** toutes vos données sont visibles dans l'application, et vous pouvez exporter vos reçus en fichier CSV (Reçus → Exporter → Exporter en CSV, qui exporte la liste affichée, filtres compris ; ou sélectionner des reçus → Exporter → Exporter en CSV). Les photos ne font pas partie de l'export.
- **Rectification :** modifiez tout reçu, catégorie, marchand ou budget dans l'application.
- **Suppression :** supprimez des éléments un par un dans l'application. Un reçu supprimé (Supprimer sur le reçu, ou sélectionner des reçus → Mettre à la corbeille) va dans la corbeille (Réglages → Corbeille), où vous pouvez le restaurer pendant 30 jours ; il est ensuite supprimé définitivement, avec sa photo, à la prochaine ouverture de l'application. Depuis la corbeille, Supprimer définitivement l'efface tout de suite. Vous pouvez aussi supprimer votre compte, dans l'application ou sur le web (section 8).
- **Opposition et limitation :** vous pouvez arrêter tout traitement dans le cloud à tout moment en vous déconnectant ou en supprimant votre compte ; l'application continue de fonctionner en local.
- **Retrait du consentement aux annonces :** voir la section 10.

Pour toute demande, contactez-nous (section 12). Vous pouvez aussi adresser une réclamation à l'autorité de protection des données de votre pays.

## 8. Suppression du compte

- **Dans l'application :** Réglages → Supprimer mon compte (visible lorsque vous êtes connecté). Une nouvelle connexion avec Google vous est demandée pour confirmer.
- **Sans l'application :** suivez les instructions de <https://talbidev.github.io/recibo-delete-account/>.

La suppression du compte efface définitivement et immédiatement votre compte, toutes vos données synchronisées, les photos de vos reçus stockées dans le cloud, votre compteur de scans et vos traces de scans bonus (aucune sauvegarde ne permet de les restaurer). Les journaux techniques du service d'extraction (conservés jusqu'à 7 jours) et les images de reçus transmises à Anthropic (conservées 30 jours au plus) expirent d'eux-mêmes après la suppression, comme décrit en section 5. Les données collectées par Google pour les vidéos publicitaires ne sont pas détenues par nous et ne sont pas concernées : voir la section 10. Les données de votre appareil ne sont pas touchées : pour les effacer aussi, désinstallez l'application ou effacez ses données dans les paramètres système d'Android (Paramètres → Applications → Recibo → Stockage → Effacer les données ; l'entrée Réglages → Effacer les données de cet appareil de l'application ouvre cet écran).

## 9. Enfants

Recibo n'est pas destinée aux enfants de moins de 13 ans, et nous ne collectons pas sciemment de données personnelles les concernant.

## 10. Publicité : vidéos avec récompense

**Quand une vidéo est proposée.** Seulement aux utilisateurs connectés, et seulement quand les scans du mois et les scans bonus sont épuisés : dans le message affiché quand un scan est refusé pour cette raison, et dans le menu d'ajout d'un reçu. Regarder une vidéo est facultatif et donne des scans bonus. Aucune vidéo n'est affichée pendant la synchronisation ni les exports, et aucune n'est nécessaire pour utiliser l'application : la saisie manuelle reste toujours possible.

**Qui traite les données.** Les vidéos sont fournies par Google AdMob. Google est un tiers indépendant qui utilise les données collectées par son SDK pour ses propres finalités (publicité, analyse, prévention des fraudes), selon ses propres règles, et non pour le compte de Recibo. Quand l'application charge ou affiche une vidéo, le SDK Google Mobile Ads collecte, selon Google : l'adresse IP de votre appareil (qui peut servir à estimer sa position approximative), vos interactions avec l'annonce (par exemple lancement de l'application, appuis et visionnages de vidéos), des informations de diagnostic et de performance sur l'application et le SDK, et des identifiants d'appareil (identifiant publicitaire Android, identifiant de groupe d'applications, « app set ID », et, le cas échéant, d'autres identifiants liés aux comptes connectés sur l'appareil). Une vidéo peut être chargée à l'avance, dès qu'elle peut être proposée, avant que vous choisissiez de la regarder.

**Ce que Recibo n'envoie pas à Google.** Aucun identifiant de compte, aucune adresse e-mail, aucune donnée de reçu. Pour créditer la récompense, Google envoie à notre service une confirmation signée qui contient le code à usage unique émis pour cette vidéo et un identifiant de transaction (section 1).

**Consentement.** Dans l'Espace économique européen, au Royaume-Uni et en Suisse, les annonces ne sont affichées qu'après votre choix dans le formulaire de consentement de Google, qui s'ouvre lors de votre premier appui sur le bouton de la vidéo. Sans consentement, aucune vidéo n'est affichée et la saisie manuelle reste possible. Vous pouvez revoir ou retirer votre choix à tout moment dans Réglages → Options de confidentialité des annonces (affiché lorsque ce choix vous concerne). Selon vos choix et les réglages publicitaires de votre appareil, Google peut afficher des annonces personnalisées ou non personnalisées.

**Vos réglages.** Vous pouvez réinitialiser ou supprimer votre identifiant publicitaire dans les paramètres d'Android (rubrique Annonces, sous Google ou Confidentialité selon l'appareil). Les données de Google, y compris leur durée de conservation, sont gérées par Google : voir comment Google utilise les informations des applications qui utilisent ses services, <https://policies.google.com/technologies/partner-sites?hl=fr>, et la politique de confidentialité de Google, <https://policies.google.com/privacy?hl=fr>.

**Scans bonus.** Les scans bonus ne peuvent servir que pendant le mois où ils ont été crédités et sont perdus à la remise à zéro mensuelle. Le nombre de scans bonus par vidéo, le nombre de vidéos par jour et la disponibilité des vidéos peuvent changer à tout moment, sans préavis. Les scans bonus déjà crédités restent utilisables jusqu'à la remise à zéro mensuelle.

## 11. Modifications de cette politique et du service

Nous pouvons mettre à jour cette politique. Les modifications seront publiées sur cette page avec une nouvelle date de mise à jour.

Le stockage dans le cloud n'est soumis à aucune limite aujourd'hui. Si une limite était un jour introduite, elle serait annoncée au moins 30 jours à l'avance, et les données que vous avez déjà ne seraient jamais supprimées pour cette raison.

## 12. Contact

Questions ou demandes : [talbidev@gmail.com](mailto:talbidev@gmail.com)
