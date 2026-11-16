# Roadmap

> **Status: draft.** This is a plan, not a schedule. Phases are ordered by dependency, not by date, and they may change as the project teaches us things.

## Guiding idea

The project is built in layers. The parts that can be tested with certainty (data, documents, schedule) come first. The voice assistant, which is the least predictable part, is built on top of a working base, so that if voice turns out to be harder than expected, the rest of the system is already useful.

The first version is only **complete** when voice works: hands-free use is the point of the project, not an extra. See [Overview](01-overview.md).

## Phases

### Phase 0: Planning and documentation *(in progress)*

- [x] First draft of the business rules ([Business rules](02-business-rules.md))
- [x] Description of how a dentist uses the app ([User flow](03-user-flow.md))
- [ ] Answer the open questions listed in those pages
- [ ] Finalize the data model (EER diagram)

### Phase 1: Data

- [ ] MySQL schema for patients, dentists, appointments, prescriptions, prescription items, protocols and prosthesis terms
- [ ] Fictional sample data for testing (never real patient data)
- [ ] Starter protocol library for implant surgery, to be reviewed by a professional of the area

### Phase 2: Document generator

- [ ] A program that takes a patient, an appointment and protocols, and produces the prescription as a PDF
- [ ] The same for prosthesis try-in terms (approved, approved with adjustments, not approved)
- [ ] The strictest-type rule and the CPF warning for controlled prescriptions

This is the heart of the system. At this stage it is driven by test input, not by voice.

### Phase 3: Basic schedule

- [ ] Book, view the day, reschedule and cancel appointments
- [ ] Mark an appointment as "in appointment" and finish it, which clears the state

### Phase 4: Voice

- [ ] Recognition of a small set of commands: choosing a protocol, term type and outcome
- [ ] Read-back and confirmation before saving
- [ ] Tests in a realistic environment (noise, mask, microphone close to the mouth)

### Phase 5: Mobile app

- [ ] Bring the schedule, the confirmation screens and voice together in one app
- [ ] Printing at the end of the appointment

### Later

- Digital signatures
- Other specialties and more document types, such as medical certificates
- Patient messages and reminders
- Procedure notes in the appointment record
- A fuller clinic management system

## Definition of done for the first version

A dentist can run a whole appointment without touching the screen or taking off their gloves:

1. The patient is already in the schedule and is marked as "in appointment"
2. The dentist asks for a prescription and a prosthesis term by voice
3. The assistant reads back each one, and the dentist confirms
4. When the dentist finishes the appointment, the documents are printed for signature

## Pending decisions

**Technology**
- How voice recognition will work, and whether it runs on the device or in the cloud (this affects privacy)
- Which kind of mobile app to build, and where the server will run
- How printing will connect

**Legal and professional review** (before any real-world use)
- Requirements for prescriptions and signatures, to be checked with the professional council and legal advice
- Compliance with Brazilian data protection law (LGPD)
- Review of the standard prosthesis term text
- Review of the protocol templates by professionals of each specialty

**Business questions** are listed in [Business rules](02-business-rules.md#open-questions) and [User flow](03-user-flow.md#open-questions).
