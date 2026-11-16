# User Flow

> **Status: draft.** This page describes how a dentist is *planned* to use the app during a day of appointments. The voice commands below are **illustrative**: the real wording will be defined and tested with real use. The app is meant to be used in Brazilian Portuguese, and the examples here are translated.

The rules behind each step are in [Business rules](02-business-rules.md).

## 1. Before the appointments: the schedule

The clinic assistant books appointments in the app's schedule, on a computer or tablet, registering new patients when needed (full name, address and main phone are required, CPF and second phone are optional). Each appointment is already linked to a registered patient, and it can be rescheduled or cancelled when plans change. The day's list is simply the day's appointments in the schedule.

This is the only part of the app that needs typing, and it happens away from the chair.

## 2. Calling the patient in

The dentist calls the next patient. At that moment, **before putting gloves on**, they mark that patient as **in appointment**, either with a tap on the list or with a short voice command such as:

> **Dentist:** Next patient.
> **Assistant:** Fulano de Tal. Confirm?
> **Dentist:** Confirm.

From now on, every document goes to this patient. The screen shows only the patient's name in large letters and a discreet sign that the assistant is available. There is nothing to tap.

## 3. During the appointment: asking for documents

The dentist works normally and asks for documents when needed. The assistant reads back what it understood, and nothing is saved until the dentist confirms.

### Prescription after implant surgery

> **Dentist:** Prescription, standard amoxicillin and standard Toragesic.
> **Assistant:** Prescription with two medications: standard amoxicillin and standard Toragesic. Confirm?
> **Dentist:** Confirm.
> **Assistant:** Prescription added to the queue.

Each name is the nickname of a protocol in the dentist's library, so the assistant fills in the medication, quantity and instructions exactly as the dentist previously reviewed them.

A protocol can be adjusted for a single prescription without changing the protocol itself:

> **Dentist:** Prescription, standard amoxicillin, but for ten days.

### Prosthesis try-in

When the try-in goes well, which is the usual case:

> **Dentist:** Try-in term, upper complete denture, approved.
> **Assistant:** Try-in term, upper complete denture, approved. Confirm?

When the patient asks for changes, the term records what was requested, in the dentist's own words:

> **Dentist:** Try-in term, upper complete denture, approved with adjustments: patient asked to change the tooth shade.
> **Assistant:** Try-in term, upper complete denture, approved with adjustments. Adjustment recorded: "patient asked to change the tooth shade". Confirm?

When the try-in is not approved, a term is still produced, with the reason recorded.

Every try-in produces a term, so the history of a prosthesis builds up over the appointments.

## 4. When something goes wrong

| Situation | What the assistant does |
|---|---|
| No patient is in appointment | Says so and creates nothing |
| A controlled prescription is requested and the patient has no CPF on file | Warns right away, so it can be completed later by the clinic assistant |
| The protocol name is not recognized | Says it did not find it and does not guess |
| The assistant misunderstood | The dentist says "correct" and repeats the request |
| The dentist forgot to mark the patient | Can name the patient by voice, and the assistant confirms the name before using it |

## 5. Finishing the appointment

> **Dentist:** Finish appointment.
> **Assistant:** Two documents ready: one prescription and one try-in term. Printing.

The documents are printed for the patient to sign on paper, and the "in appointment" state is **cleared**. Documents can never end up on the previous patient's record.

## 6. What the screen shows

The screen is for checking, not for working:

- **Waiting:** the patient's name and a sign that the assistant is available
- **Confirmation:** what the assistant understood, in large text readable from a distance. The assistant also says it aloud
- **Queue:** a short list of the documents created in this appointment
- **Settings screens** (protocol library, patient registration, clinic details) are used outside appointments, with no gloves

## Open questions

1. **How does listening start?** Options include a spoken wake word detected on the device, or a button on a headset. This affects privacy and reliability.
2. **Microphone.** Suction, handpieces and a mask make voice recognition hard. A microphone close to the mouth, such as a headset, is likely needed.
3. **Cancelling and reviewing.** Commands such as "cancel the last document" or "read the queue" need to be defined.
4. **Printing.** Which printer, and how the app connects to it.
