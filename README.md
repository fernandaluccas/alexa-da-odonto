# Dental Voice Assistant

> **Status: early design phase.** There is no working code yet. This repository currently documents the idea, the business rules and the planned database design. Everything described here is **planned, not implemented**.

*"Dental Voice Assistant" is a working title and may change.*

## What is it?

A hands-free voice assistant for dentists.

Many dentists work alone or with a single assistant, and a lot of chair-side time goes to paperwork: prescriptions, prosthesis forms and patient-record documents. The idea is simple: during an appointment, the dentist asks the assistant to prepare a document for the patient currently being treated (for example, *"prescription with the standard amoxicillin"*). The assistant fills in the right template, keeps it in a queue, and everything is printed at the end of the appointment.

## Why hands-free?

The dentist is usually wearing gloves and in the middle of a procedure. If using the app means typing or touching a screen, it is no better than writing the documents on a computer after the appointment, which is exactly what happens today. Voice is the product, not an extra.

## Planned scope: first version

- Patient records and a basic schedule: book appointments, see the day's patients, reschedule and cancel. Each appointment is already linked to its patient
- A library of medication protocols per specialty, starting with implant surgery prescriptions, reviewed and accepted by each dentist
- Prescriptions (simple and controlled) with one or more medications
- Prosthesis try-in and acceptance forms (approved / approved with adjustments / not approved)
- PDF generation and printing, with paper signatures

**Not in the first version:** digital signatures, other specialties, patient messaging and reminders, advanced scheduling features, and other documents such as medical certificates.

## Design principles

1. **Hands-free first.** Nothing that happens during an appointment should require typing or touching the screen.
2. **No invented clinical content.** The assistant only selects from protocols the dentist has already reviewed and accepted. It never fills in doses or instructions on its own.
3. **Confirm before saving.** The assistant reads back what it understood, and the dentist confirms.
4. **Always know who is in the chair.** Documents are attached to the patient marked as "in appointment". With no patient in appointment, no document is created.
5. **Collect only what is needed.** Patient data is health data and is subject to Brazilian data protection law (LGPD).
6. **Everything is documented and signed** by the patient.

## How it will work (planned)

1. The clinic assistant books appointments in the schedule, and the day's patients are listed from it.
2. The dentist calls the patient and marks them as "in appointment".
3. During the appointment, the dentist asks for documents by voice, choosing from known protocols and templates.
4. The assistant reads back what it understood, and the dentist confirms.
5. When the appointment is finished, the documents are printed for signature.

## Planned data model

```
patient ──< appointment ──< prescription ──< prescription_item >── protocol
                │
                ├──< prosthesis_term
                │
dentist ────────┘
```

Main rules decided so far:

- Each patient has a system-generated numeric ID. The CPF (Brazilian individual taxpayer ID) is optional, because it is only required on some prescriptions.
- A prescription can have several medications. It takes the **strictest** type among them: if one medication is controlled, the whole prescription is controlled.
- Controlled prescriptions require the patient's CPF. The assistant warns if it is missing.
- Every prosthesis try-in generates a signed term, whether it was approved or not, so each case builds a timeline.
- Updates to template protocols never change what a dentist has already accepted.

Identifiers in the actual schema may be in Portuguese.

## Planned technology

- **Database:** MySQL
- **Document generation:** Python (planned)
- **Voice and mobile app:** to be decided

## Roadmap

- [x] Idea and first draft of the business rules
- [ ] Finalize the data model (EER diagram)
- [ ] MySQL schema
- [ ] Document generator (PDF prescriptions and terms)
- [ ] Voice command prototype
- [ ] Mobile app and basic schedule
- [ ] Later: digital signatures, other specialties, patient messaging

## Privacy and safety

- **No real patient data belongs in this repository**, including for testing. Use fictional data only.
- This project is not a medical device and does not give clinical advice. The content of every protocol is the responsibility of the dentist who accepts it.
- Legal requirements for prescriptions and signatures must be checked with the relevant professional council and legal advice before any real-world use.

## Repository structure (planned)

```
docs/        business rules and diagrams
database/    schema and fictional sample data
src/         application code (not started)
```

## Contributing and license

The project is not open for contributions yet. License: to be decided.
