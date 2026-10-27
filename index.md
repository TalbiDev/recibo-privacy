---
title: Privacy Policy — Recibo
---

# Privacy Policy — Recibo

Last updated: 2026-10-26

This policy describes how the Android app **Recibo** (receipt-based expense tracking), developed by T.Dev, handles your data. *Une version française suit la version anglaise.*

In short: Recibo works fully offline without an account. An account (Sign in with Google) is optional and only needed to scan receipts automatically and to back up and sync your data to the cloud. Recibo contains no advertising and no analytics, and your data is never sold.

**Data controller:** Said Talbi (T.Dev). Contact: [talbidev@gmail.com](mailto:talbidev@gmail.com)

## 1. Data we collect

**Without an account**, everything you enter stays on your device: receipts (amount, currency, merchant, category, day, payment method, note, photo), budgets, categories, merchant classification rules and settings. Nothing is sent to us. Automatic scanning is not available without an account; manual entry remains fully available.

**With an account**, we process:

- **Account data, received from Google when you sign in** and stored by our authentication service (Supabase Auth): your email address, your full name, the URL of your profile photo and your Google account identifier, together with a unique Recibo account identifier.
- **Synced data:** your receipts (day, total amount, tax amount, currency, payment method, merchant, category, note, processing status, extraction confidence scores and suggested category), merchants, merchant classification rules, custom categories and budgets, together with creation, modification and deletion dates.
- **Receipt photos**, uploaded to private cloud storage as part of sync.
- **Scan usage:** a monthly counter of the number of automatic scans used by your account (a limited monthly allowance shown in the app).
- **Receipts sent for scanning:** when you scan or import a receipt, its image is sent to our extraction service to read the amount, merchant, date and so on (see section 3). Capturing and cropping the receipt happen on your device; only the receipt image is sent.
- **Technical logs of the extraction service:** time of the request, a truncated IP address (last part of an IPv4 address, last half of an IPv6 address masked), request size, response status, response time, a short irreversible fingerprint of your account identifier, the outcome of access checks (identity check, refusal reason, rate-limit decision), and technical error events of the scan counter or of the AI service (event name, error cause, status code). These logs never contain the image, the extracted data, your email address or your account identifier in clear.

**Data that stays on your device only, even with an account:** your preferences (display currency, language, scan reminder, onboarding state), the home-screen widget's state, budget alert history, and the state of financial advice cards.

## 2. Why we use it

- To provide the app: store, display and compute your expenses (all totals and statistics are calculated on your device).
- To read receipts automatically when you scan them.
- To back up your data and sync it between your devices when you are signed in.
- To enforce the monthly scan allowance and protect the service from abuse (rate limiting).
- To diagnose errors in the extraction service.

**Legal bases:** performance of the service you request (account, sync, receipt reading, scan allowance); legitimate interest (abuse prevention, rate limiting, technical logs, diagnostics).

We do not use your data for advertising, profiling, or to train AI models, and we do not sell it.

## 3. Storage and service providers

- **Supabase** (database, authentication, file storage) hosts your account, your synced data, your receipt photos and your scan counter. The production project is hosted in the eu-central-1 region (Frankfurt, European Union). Data is encrypted in transit (TLS) and at rest (AES-256). Currently, our database has no managed backups: when your account is deleted, the deletion is final immediately. Privacy policy: <https://supabase.com/privacy>
- **Cloudflare** (Workers) runs the extraction service that receives a receipt image, forwards it for reading and returns the result. The image is not stored. Its technical logs (section 1) are kept for up to 7 days. Privacy policy: <https://www.cloudflare.com/privacypolicy/>
- **Anthropic** (Claude API) reads the receipt image and returns the extracted fields. Only the image and a fixed instruction are sent: no account identifier, email address or other data. Anthropic does not use this data to train its models and deletes it within 30 days, unless it must be kept to comply with the law or because it was flagged for abuse. Privacy policy: <https://www.anthropic.com/legal/privacy>
- **Google** provides Sign in with Google (through Android's Credential Manager) and the on-device document scanner (ML Kit, Google Play services) used to capture receipts. The scanner captures and crops the receipt on your device; the resulting image is then handled by Recibo as described above. Privacy policy: <https://policies.google.com/privacy>
- **Android backup** (Google): if you have Android backup turned on, Recibo's local database and settings may be included in your device backup (see section 6).

## 4. International transfers

Your account, synced data and receipt photos are hosted by Supabase in the European Union (Frankfurt). Cloudflare (global network), Anthropic (United States) and Google may process data outside your country, under their respective data processing terms.

## 5. Retention

- **On your device:** until you delete it in the app, erase the app's data or uninstall the app.
- **In the cloud:** for as long as your account exists. A receipt you delete permanently has its photo removed from cloud storage; a minimal record of the deletion is kept so that your other devices also remove it, until your account is deleted.
- **Scan counter:** one row per month, kept until your account is deleted.
- **Extraction service logs:** kept for up to 7 days.
- **Receipt images sent for scanning:** not stored by our extraction service; deleted by Anthropic within 30 days (see section 3).
- **Backups:** currently, our database has no managed backups, so no copy of your cloud data remains in a backup after your account is deleted.

## 6. Security

- All traffic between the app and our services uses encrypted connections (HTTPS, TLS). The Supabase database and file storage are encrypted at rest (AES-256).
- Access rules in the database (row-level security) ensure that each account can only read and write its own data. Receipt photos are stored in a private bucket, never reachable by a public link.
- On your device, receipt photos are stored in the app's private storage, never in your public gallery.
- Android cloud backup is limited to Recibo's database and settings, and only when the backup can be end-to-end encrypted (a screen lock is set); receipt photos and sign-in tokens are excluded. On Android 8.0 and 8.1, backup is turned off.
- The app contains no API key for the AI service: it is held only by our extraction service.

## 7. Your rights

Depending on where you live, you have the right to:

- **Access and portability:** all your data is visible in the app, and you can export your receipts as a CSV file (Receipts → Export → Export as CSV, which exports the current, filtered list; or select receipts → Export → Export as CSV). Photos are not included in the export.
- **Rectification:** edit any receipt, category, merchant or budget in the app.
- **Deletion:** delete individual items in the app, or delete your account (section 8).
- **Objection and restriction:** you can stop all cloud processing at any time by signing out or deleting your account; the app keeps working locally.

For any request, contact us (section 12). You may also lodge a complaint with your local data protection authority.

## 8. Deleting your account

- **In the app:** Settings → Delete my account (visible when signed in). You will be asked to sign in with Google again to confirm.
- **Without the app:** follow the instructions at <https://talbidev.github.io/recibo-delete-account/>.

Deleting your account permanently and immediately removes your account, all your synced data, your receipt photos stored in the cloud and your scan counter (there is no backup from which they could be restored). The extraction service's technical logs (kept for up to 7 days) and the receipt images sent to Anthropic (kept for 30 days at most) expire on their own after the deletion, as described in section 5. The data on your device is not touched: to remove it too, uninstall the app or clear its data in Android's system settings (Settings → Apps → Recibo → Storage → Clear data; the in-app entry Settings → Erase this device's data opens this screen).

## 9. Children

Recibo is not directed at children under 13, and we do not knowingly collect personal data from them.

## 10. No advertising, no analytics

Recibo contains no advertising SDK and no analytics or tracking SDK. Your data is never sold or shared for advertising.

## 11. Changes to this policy

We may update this policy. Changes will be posted on this page with a new "Last updated" date.

## 12. Contact

Questions or requests: [talbidev@gmail.com](mailto:talbidev@gmail.com)

---

# Politique de confidentialité (français)

Dernière mise à jour : 2026-10-26

Cette politique décrit la manière dont l'application Android **Recibo** (suivi de dépenses à partir de reçus), développée par T.Dev, traite vos données.

En bref : Recibo fonctionne entièrement hors ligne, sans compte. Un compte (connexion avec Google) est facultatif : il n'est nécessaire que pour scanner automatiquement les reçus et pour sauvegarder et synchroniser vos données dans le cloud. Recibo ne contient ni publicité ni outil de mesure d'audience, et vos données ne sont jamais vendues.

**Responsable du traitement :** Said Talbi (T.Dev). Contact : [talbidev@gmail.com](mailto:talbidev@gmail.com)

## 1. Données collectées

**Sans compte**, tout ce que vous saisissez reste sur votre appareil : reçus (montant, devise, marchand, catégorie, jour, moyen de paiement, note, photo), budgets, catégories, règles de classement des marchands et réglages. Rien ne nous est envoyé. Le scan automatique n'est pas disponible sans compte ; la saisie manuelle reste entièrement disponible.

**Avec un compte**, nous traitons :

- **Données du compte, reçues de Google à la connexion** et conservées par notre service d'authentification (Supabase Auth) : votre adresse e-mail, votre nom complet, l'URL de votre photo de profil et l'identifiant de votre compte Google, ainsi qu'un identifiant de compte Recibo unique.
- **Données synchronisées :** vos reçus (jour, montant total, montant de taxe, devise, moyen de paiement, marchand, catégorie, note, statut de traitement, indices de confiance de l'extraction et catégorie suggérée), marchands, règles de classement, catégories personnalisées et budgets, avec leurs dates de création, de modification et de suppression.
- **Photos des reçus**, envoyées dans un stockage cloud privé lors de la synchronisation.
- **Consommation de scans :** un compteur mensuel du nombre de scans automatiques utilisés par votre compte (un nombre limité de scans par mois, affiché dans l'app).
- **Reçus envoyés au scan :** quand vous scannez ou importez un reçu, son image est envoyée à notre service d'extraction pour en lire le montant, le marchand, la date, etc. (voir section 3). La capture et le recadrage du reçu se font sur votre appareil ; seule l'image du reçu est envoyée.
- **Journaux techniques du service d'extraction :** heure de la requête, adresse IP tronquée (dernière partie d'une adresse IPv4, seconde moitié d'une adresse IPv6 masquées), taille de la requête, statut et durée de la réponse, une empreinte courte et irréversible de votre identifiant de compte, le résultat des contrôles d'accès (vérification de l'identité, motif d'un refus, décision de la limitation de débit) et les événements d'erreur technique du compteur de scans ou du service d'IA (nom de l'événement, cause de l'erreur, code de statut). Ces journaux ne contiennent jamais l'image, les données extraites, votre adresse e-mail ni votre identifiant de compte en clair.

**Données qui restent sur votre appareil, même avec un compte :** vos préférences (devise d'affichage, langue, rappel de scan, état de l'accueil), l'état du widget d'écran d'accueil, l'historique des alertes de budget et l'état des cartes de conseils.

## 2. Finalités

- Fournir l'application : enregistrer, afficher et calculer vos dépenses (tous les totaux et statistiques sont calculés sur votre appareil).
- Lire automatiquement les reçus que vous scannez.
- Sauvegarder vos données et les synchroniser entre vos appareils lorsque vous êtes connecté.
- Appliquer le quota mensuel de scans et protéger le service contre les abus (limitation de débit).
- Diagnostiquer les erreurs du service d'extraction.

**Bases légales :** exécution du service que vous demandez (compte, synchronisation, lecture des reçus, quota de scans) ; intérêt légitime (prévention des abus, limitation de débit, journaux techniques, diagnostic).

Nous n'utilisons pas vos données pour la publicité, le profilage ou l'entraînement de modèles d'IA, et nous ne les vendons pas.

## 3. Stockage et sous-traitants

- **Supabase** (base de données, authentification, stockage de fichiers) héberge votre compte, vos données synchronisées, les photos de vos reçus et votre compteur de scans. Le projet de production est hébergé dans la région eu-central-1 (Francfort, Union européenne). Les données sont chiffrées en transit (TLS) et au repos (AES-256). Actuellement, notre base de données n'a pas de sauvegarde gérée : quand votre compte est supprimé, la suppression est définitive immédiatement. Politique de confidentialité : <https://supabase.com/privacy>
- **Cloudflare** (Workers) exécute le service d'extraction, qui reçoit l'image d'un reçu, la transmet pour lecture et renvoie le résultat. L'image n'est pas conservée. Ses journaux techniques (section 1) sont conservés jusqu'à 7 jours. Politique de confidentialité : <https://www.cloudflare.com/privacypolicy/>
- **Anthropic** (API Claude) lit l'image du reçu et renvoie les champs extraits. Seuls l'image et une consigne fixe sont envoyés : aucun identifiant de compte, aucune adresse e-mail, aucune autre donnée. Anthropic n'utilise pas ces données pour entraîner ses modèles et les supprime dans un délai de 30 jours, sauf obligation légale ou signalement d'abus. Politique de confidentialité : <https://www.anthropic.com/legal/privacy>
- **Google** fournit la connexion avec Google (via le Credential Manager d'Android) et le scanner de documents sur l'appareil (ML Kit, services Google Play) utilisé pour photographier les reçus. Le scanner capture et recadre le reçu sur votre appareil ; l'image obtenue est ensuite traitée par Recibo comme décrit ci-dessus. Politique de confidentialité : <https://policies.google.com/privacy>
- **Sauvegarde Android** (Google) : si la sauvegarde Android est activée, la base locale et les réglages de Recibo peuvent faire partie de la sauvegarde de votre appareil (voir section 6).

## 4. Transferts internationaux

Votre compte, vos données synchronisées et les photos de vos reçus sont hébergés par Supabase dans l'Union européenne (Francfort). Cloudflare (réseau mondial), Anthropic (États-Unis) et Google peuvent traiter des données hors de votre pays, selon leurs conditions de traitement des données respectives.

## 5. Conservation

- **Sur votre appareil :** jusqu'à ce que vous les supprimiez dans l'application, effaciez les données de l'application ou la désinstalliez.
- **Dans le cloud :** tant que votre compte existe. Un reçu supprimé définitivement voit sa photo retirée du stockage cloud ; une trace minimale de la suppression est conservée, pour que vos autres appareils le suppriment aussi, jusqu'à la suppression de votre compte.
- **Compteur de scans :** une ligne par mois, conservée jusqu'à la suppression du compte.
- **Journaux du service d'extraction :** conservés jusqu'à 7 jours.
- **Images envoyées au scan :** non conservées par notre service d'extraction ; supprimées par Anthropic dans un délai de 30 jours (voir la section 3).
- **Sauvegardes :** actuellement, notre base de données n'a pas de sauvegarde gérée ; aucune copie de vos données cloud ne subsiste donc dans une sauvegarde après la suppression de votre compte.

## 6. Sécurité

- Tous les échanges entre l'application et nos services passent par des connexions chiffrées (HTTPS, TLS). La base et le stockage de fichiers Supabase sont chiffrés au repos (AES-256).
- Des règles d'accès dans la base (sécurité au niveau des lignes, RLS) garantissent que chaque compte ne peut lire et écrire que ses propres données. Les photos des reçus sont stockées dans un espace privé, jamais accessible par un lien public.
- Sur votre appareil, les photos des reçus sont stockées dans l'espace privé de l'application, jamais dans votre galerie publique.
- La sauvegarde cloud d'Android se limite à la base et aux réglages de Recibo, et seulement si elle peut être chiffrée de bout en bout (verrouillage d'écran configuré) ; les photos des reçus et les jetons de connexion en sont exclus. Sous Android 8.0 et 8.1, la sauvegarde est désactivée.
- L'application ne contient aucune clé d'API du service d'IA : seule notre service d'extraction la détient.

## 7. Vos droits

Selon votre lieu de résidence, vous disposez des droits suivants :

- **Accès et portabilité :** toutes vos données sont visibles dans l'application, et vous pouvez exporter vos reçus en fichier CSV (Reçus → Exporter → Exporter en CSV, qui exporte la liste affichée, filtres compris ; ou sélectionner des reçus → Exporter → Exporter en CSV). Les photos ne font pas partie de l'export.
- **Rectification :** modifiez tout reçu, catégorie, marchand ou budget dans l'application.
- **Suppression :** supprimez des éléments un par un dans l'application, ou supprimez votre compte (section 8).
- **Opposition et limitation :** vous pouvez arrêter tout traitement dans le cloud à tout moment en vous déconnectant ou en supprimant votre compte ; l'application continue de fonctionner en local.

Pour toute demande, contactez-nous (section 12). Vous pouvez aussi adresser une réclamation à l'autorité de protection des données de votre pays.

## 8. Suppression du compte

- **Dans l'application :** Réglages → Supprimer mon compte (visible lorsque vous êtes connecté). Une nouvelle connexion avec Google vous est demandée pour confirmer.
- **Sans l'application :** suivez les instructions de <https://talbidev.github.io/recibo-delete-account/>.

La suppression du compte efface définitivement et immédiatement votre compte, toutes vos données synchronisées, les photos de vos reçus stockées dans le cloud et votre compteur de scans (aucune sauvegarde ne permet de les restaurer). Les journaux techniques du service d'extraction (conservés jusqu'à 7 jours) et les images de reçus transmises à Anthropic (conservées 30 jours au plus) expirent d'eux-mêmes après la suppression, comme décrit en section 5. Les données de votre appareil ne sont pas touchées : pour les effacer aussi, désinstallez l'application ou effacez ses données dans les paramètres système d'Android (Paramètres → Applications → Recibo → Stockage → Effacer les données ; l'entrée Réglages → Effacer les données de cet appareil de l'application ouvre cet écran).

## 9. Enfants

Recibo n'est pas destinée aux enfants de moins de 13 ans, et nous ne collectons pas sciemment de données personnelles les concernant.

## 10. Ni publicité, ni mesure d'audience

Recibo ne contient aucun SDK publicitaire ni aucun SDK de mesure d'audience ou de suivi. Vos données ne sont jamais vendues ni partagées à des fins publicitaires.

## 11. Modifications

Nous pouvons mettre à jour cette politique. Les modifications seront publiées sur cette page avec une nouvelle date de mise à jour.

## 12. Contact

Questions ou demandes : [talbidev@gmail.com](mailto:talbidev@gmail.com)
