# HabitGame

Android aplikacija za praćenje navika i obaveza u obliku igrice, urađena u okviru predmeta
**Mobilne aplikacije** (tim 19, 2025).

## O projektu

HabitGame pretvara svakodnevne obaveze u igru. Korisnik pravi zadatke (jednokratne i ponavljajuće),
razvrstava ih po kategorijama i za svaki urađen zadatak dobija iskustvene poene (XP). Sakupljanjem XP-a
raste nivo, a na kraju svakog nivoa čeka bitka sa bosom u kojoj se osvaja novac i oprema. Novac se troši u
prodavnici, a oprema pojačava napad. Korisnici mogu da dodaju prijatelje (i skeniranjem QR koda), osnivaju
saveze, šalju poruke i dobijaju push notifikacije.

Projekat se sastoji iz dva dela:
- `HabitGame` – Android aplikacija (Java),
- `FcmServer` – mali Node.js server za slanje push notifikacija (Firebase Cloud Messaging).

## Tehnologije

- Java, Android Studio, Android Navigation (fragmenti)
- Firebase Authentication, Cloud Firestore, Cloud Messaging
- Node.js (`FcmServer`)
- Biblioteke: Lottie (animacije), MPAndroidChart (grafikoni), Kizitonwose Calendar i Android Week View
  (kalendar), ZXing (QR kodovi), OkHttp

## Funkcionalnosti

- Registracija, aktivacija naloga putem linka, prijava, promena lozinke
- Profil, pretraga korisnika, prijatelji (uključujući dodavanje QR kodom)
- Savezi, pozivnice, poruke i push notifikacije
- Kategorije i zadaci, ponavljajući zadaci, kalendarski prikaz
- XP, nivoi i titule, bitka sa bosom, prodavnica i oprema
- Statistika i prikaz napretka

## Moj doprinos

Autor sam sledećih funkcionalnosti (drugi deo aplikacije radio je kolega, v. ispod).

### 1. Kategorije
- Kreiranje, izmena i prikaz kategorija zadataka, sa izborom boje (`CategoryCreationFragment`,
  `CategoryEditBottomSheet`, `CategoryListFragment`, `CategoryAdapter`, `CategoryService`, `CategoryRepository`).

### 2. Zadaci
- Kreiranje zadatka sa kategorijom, težinom, bitnošću i datumom izvršenja (`TaskCreationFragment`).
- Izmena zadatka (`EditTaskFragment`), prikaz detalja (`TaskDetailsBottomSheet`) i liste zadataka (`TaskListFragment`).
- Statusi zadatka: aktivan, urađen, neurađen, otkazan i pauziran. Zadatak se označava kao urađen ili otkazan
  (`TaskService`), a neizvršeni zadaci se automatski prebacuju u status "neurađen".
- Kalendarski prikazi zadataka: dnevni/nedeljni i mesečni (`TasksCalendarFragment`, `TasksMonthFragment`,
  `TasksPagerFragment`).

### 3. Ponavljajući zadaci
- Kreiranje i izmena ponavljajućih zadataka (`RepeatedTaskCreateFragment`, `RepeatedTaskEditFragment`).
- Generisanje pojedinačnih pojavljivanja po rasporedu (`RepeatedTaskService`, `RepeatedTaskOccurrenceService`,
  `RecurrenceScheduler`) i njihov prikaz i obrada (`RepeatedTaskOccurrenceListFragment`,
  `RepeatedTaskOccurrenceDetailsBottomSheet`).

### 4. XP, nivoi i statistika uspeha
- Obračun XP-a na osnovu težine, bitnosti i trenutnog nivoa (`XpCalculator`).
- Napredovanje kroz nivoe, prag XP-a po nivou, titule, nagrade u novcu i rast snage (`LevelUtils`).
- Dodavanje XP-a i provera prelaska na sledeći nivo pri završetku zadatka (`AccountRepository`).
- Procenat uspešnosti zadataka u toku etape, uz poštovanje kvote (`StageMetricsService`).

### 5. Bitka sa bosom (`BattleFragment`)
- Boss sa životnim poenima koji zavise od nivoa, i šansa pogotka računata iz uspešnosti zadataka.
- Napad dugmetom ili **potresom telefona** (akcelerometar).
- Animacije (Lottie) i zvučni efekti, ograničen broj pokušaja.
- Sanduk sa nagradom (novac i oprema) koji se otvara nakon pobede.

### 6. Prodavnica
- Deo logike kupovine i primene opreme (`ShopFragment`).

## Pokretanje

1. Otvoriti folder `HabitGame` u **Android Studiju** i sačekati Gradle sinhronizaciju.
2. Dodati sopstveni `google-services.json` iz Firebase konzole u `HabitGame/app/`.
3. Povezati telefon sa uključenim *USB debugging*-om (ili pokrenuti emulator) i kliknuti **Run**.
4. Za push notifikacije pokrenuti `FcmServer` (`npm install`, zatim `node index.js`) sa Firebase servisnim nalogom.
