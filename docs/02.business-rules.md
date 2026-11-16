# Business Rules

> **Status: draft.** These rules describe how the app is *planned* to behave. Nothing here is implemented yet, and some points are still open (see [Open questions](#open-questions)).

This page collects the rules that shape the first version of the Dental Voice Assistant. The database design and the code will be built to follow them.

## 1. Patients

- **BR-01.** Each patient has a system-generated numeric ID. It is the only thing other records use to point to a patient.
- **BR-02.** A patient record holds a full name, an address and a main phone number (all required), plus a second phone number and a CPF (both optional). The CPF is the Brazilian individual taxpayer ID.
- **BR-03.** The CPF is optional because only some prescriptions require it. A patient without a CPF can still be registered and treated.
- **BR-04.** The app collects only the data that documents actually use.

## 2. Protocol library

A *protocol* is a ready-made medication entry, such as "standard amoxicillin", that the dentist can request by a short spoken name.

- **BR-05.** Each protocol holds the medication name with its strength, the total quantity, the instructions for the patient (dosage text), a spoken nickname and a type (`simple` or `controlled`). Quantity and instructions are stored exactly as they should be printed.
- **BR-06.** Nicknames are unique, so a spoken name never points to two protocols.
- **BR-07.** The library comes with **template protocols by specialty** as a starting point, so a dentist does not begin from an empty list.
- **BR-08.** Template protocols are not active until the dentist **reviews and accepts** them. The dentist can edit them or add their own.
- **BR-09.** The assistant never invents or completes clinical content. It only uses protocols the dentist has accepted, and the dentist is responsible for their content.
- **BR-10.** A template update never changes a protocol the dentist has already accepted. The dentist is told a new version exists and decides whether to review it.
- **BR-11.** Template protocols must be reviewed by professionals from the relevant specialty before being offered.

## 3. Prescriptions

- **BR-12.** A prescription belongs to one appointment, and therefore to one patient and one dentist.
- **BR-13.** A prescription can contain one or more medications, each one taken from a protocol.
- **BR-14.** A prescription takes the **strictest type** among its medications. If one medication is controlled, the whole prescription is controlled. There is no need to split it into two.
- **BR-15.** A controlled prescription requires the patient's CPF. If it is missing, the app warns the dentist right away, so the problem is not discovered at printing time.
- **BR-16.** The dentist can adjust a protocol for a single prescription (for example, a different number of days) without changing the protocol itself.

## 4. Prosthesis terms

- **BR-17.** Every prosthesis try-in produces a term, whatever the outcome. Everything done must be documented and signed by the patient.
- **BR-18.** The outcome of a try-in is one of: **approved**, **approved with adjustments**, or **not approved**.
- **BR-19.** In the usual case (approved as is) the standard term text is used. When there are adjustments or the try-in is not approved, the term records what the patient asked for, such as a change of tooth shade or of vertical dimension.
- **BR-20.** Adjustment details are recorded exactly as the dentist said them. The assistant does not reword them.
- **BR-21.** A prosthesis can have several terms over time (for example, two try-ins and a final acceptance), so each case builds a timeline.
- **BR-22.** The standard text of a term is a legal-style document and must be reviewed before it becomes the default.

## 5. Appointments and voice

- **BR-23.** An appointment links one patient and one dentist, on a given day and time. Prescriptions and terms belong to an appointment.
- **BR-24.** The clinic assistant books appointments in the schedule, and the day's list is built from it, with each appointment already linked to its patient. The dentist marks a patient as **in appointment** when calling them in, before putting gloves on.
- **BR-25.** The assistant always works on the patient currently in appointment. If nobody is in appointment, it says so and creates nothing.
- **BR-26.** Finishing the appointment clears that state, so documents never end up on the previous patient's record.
- **BR-27.** Voice requests only choose between things the app already knows (protocols, term types). They are not free-form dictation.
- **BR-28.** Before saving anything, the assistant reads back what it understood, and the dentist confirms or corrects.
- **BR-29.** As a fallback, the dentist can name the patient by voice, and the assistant confirms the name before using it.
- **BR-30.** Documents are printed at the end of the appointment. Signatures are made on paper in the first version.

## 6. Privacy

- **BR-31.** Patient information is health data and is handled under Brazilian data protection law (LGPD).
- **BR-32.** Listening only starts through an explicit trigger. The app does not record the clinic continuously.
- **BR-33.** Documents and patient records are kept for a long time, so storage must be reliable and protected.

## 7. Schedule

- **BR-34.** The schedule holds appointments. Each one has a patient, a dentist, a date, a time and a status (for example: scheduled, in appointment, done, cancelled).
- **BR-35.** Booking an appointment links it to a registered patient, so nobody has to identify the patient again on the day.
- **BR-36.** An appointment can be rescheduled by changing its date and time. It stays linked to the same patient.
- **BR-37.** A cancelled appointment is marked as cancelled, not deleted.
- **BR-38.** The first version includes only this basic schedule. Reminders and confirmation messages to patients are left for later.

## Open questions

1. **Clinic header.** The dentist's name, council number (CRO) and clinic address appear on every document. Who sets them up, and where?
2. **Editing issued documents.** Can a printed document be changed afterwards, or is a new one always created? For signed documents, creating a new one is likely the safer choice.
3. **Antimicrobials.** Some prescriptions may need two copies. Is that a printing rule tied to the protocol type?
4. **Medical certificates.** Do they belong in the first version or later?
5. **Number of dentists.** The data model already has a dentist table. Is the app for a single clinic with several dentists, or for many independent dentists, each with their own library and patients?
6. **Procedure notes.** Should an appointment also record what was done? It would be a free-text field on the appointment, but it is not part of the first version.
7. **Schedule conflicts.** If two patients are booked at the same time with the same dentist, should the app block it or only warn?
