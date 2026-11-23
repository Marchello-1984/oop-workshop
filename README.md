# OOP-WORKSHOP

---

## Table of Contents
* [Functional Requirements](#functional-requirements)
  * [Media Types & Attributes](#media-types--attributes)
  * [Borrowing & Rating System](#borrowing--rating-system)
  * [User Roles & Permissions](#user-roles--permissions)
* [Non-Functional Requirements](#non-functional-requirements)
* [System Architecture & Verb-Noun Analysis](#system-architecture--verb-noun-analysis)
  * [Candidate Nouns (Domain Entities & Layers)](#candidate-nouns-domain-entities--layers)
  * [Candidate Verbs (Methods & Capability Interfaces)](#candidate-verbs-methods--capability-interfaces)

---

## Functional Requirements

### Media Types & Attributes
* **E-book**
  * **Attributes:** title, author, language, number of pages, year of publication, ISBN
  * **Actions:** view, download, read
* **Movie**
  * **Attributes:** title, director, genres, release year, language, duration
  * **Actions:** watch, download
* **Song**
  * **Attributes:** title, composer, singer, genre, file type, duration, language
  * **Actions:** play, download
* **Video-game**
  * **Attributes:** title, genre, publisher, release year, supported platforms
  * **Actions:** download, play, complete
* **App**
  * **Attributes:** title, version, publisher, supported platforms, file size
  * **Actions:** download, execute
* **Podcast**
  * **Attributes:** title, release year, host(s), guest(s), episode number, language
  * **Actions:** download, listen to episode, complete
* **Image**
  * **Attributes:** title, resolution, file format, file size, date taken
  * **Actions:** download, display

### Borrowing & Rating
* Users can borrow media items.
* Only users who have borrowed an item may rate it.

### User Roles & Startup
* Support Admin, Employee, and Borrower with name, age, and social security number.
* Prompt for role on startup (authentication is not required initially).

### Role Permissions
* **Borrower:** list items by type, select/preview details, rate borrowed items, and run media-specific actions.
* **Employee:** add or remove media items.
* **Admin:** all Employee rights plus view, create, delete, and update Borrower and Employee personal information.

---

## Non-Functional Requirements

* **Input Validation & Error Handling:** Console UI guides users with clear instructions, validates all inputs, and blocks invalid inputs/actions.
* **Extensibility & Clean Architecture:** Easy to add new media types, user roles, or capabilities without breaking existing code, structured into Presentation, Domain, and Data Access/Persistence layers.
* **Clean Builds & Version Control:** Code compiles cleanly without warnings and is pushed to GitHub (preferably on a non-main branch).

---

## Verb-Noun Analysis

### Candidate Nouns (Classes / Value Objects / Collections)
* **Library:** catalog, users, borrowing/rating records, sorting, persistence coordination
* **MediaItem (abstract base):** Id, Title, ReleaseYear, IsBorrowed, BorrowedBySsn, DueDate, ratings
  * **Concrete Media:** EBook, Movie, Song, VideoGame, AppMedia, Podcast, ImageMedia
* **User (abstract base):** Name, Age, SocialSecurityNumber, Username, PasswordHash
  * **Concrete Users:** Borrower, Employee, Admin
* **Rating:** reviewer SSN, score, optional comment
* **Presentation:** ConsoleUi, InputValidator
* **Persistence / DataAccess:** JsonDataStore, CsvDataStore

### Candidate Verbs (Methods / Capability Interfaces)
* **Borrow / Return:** `Borrow()`, `ReturnItem()`, check availability & due date
* **Rate (`IRatable`):** `AddRating(...)`, `AverageRating`
* **Download (`IDownloadable`):** `Download()`
* **View / Display / Preview (`IViewable`):** `View()`, `Display()`
* **Read (`IReadable`):** `Read()`
* **Watch (`IWatchable`):** `Watch()`
* **Play (`IPlayable`):** `Play()`
* **Complete (`ICompletable`):** `Complete()`
* **Execute (`IExecutable`):** `Execute()`
* **Listen (`IListenable`):** `Listen()`
* **Manage Collection & Users:** `AddMedia`, `RemoveMedia`, `ListByType`, `SortMedia`, `CreateUser`, `UpdateUser`, `DeleteUser`, `Authenticate`[cite: 1]
