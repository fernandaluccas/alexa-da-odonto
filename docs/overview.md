# Overview

> **Status: early design phase.** This page describes the idea behind the project. Nothing described here is implemented yet.

## The problem

Many dentists work alone or with a single assistant. During and after each appointment there is a steady stream of paperwork: prescriptions, prosthesis forms, documents for the patient record. Today this is usually done in one of two ways:

- **After the appointment, on a computer.** It adds extra time to the day, and details can be forgotten or mixed up by then.
- **During the appointment, by hand.** It interrupts the procedure, and it is hard to do with gloves on and instruments in use.

Either way, time that could go to patients goes to paperwork.

## The idea

A voice assistant that the dentist can talk to while working. Think of it as **a queue of documents that builds itself during the appointment**.

The dentist asks for a document, the assistant prepares it for the patient currently in the chair, and keeps it. At the end of the appointment, everything is printed, ready for signature.

An illustrative example (the final wording of commands is still to be defined):

> **Dentist:** Prescription, standard amoxicillin and standard painkiller.
> **Assistant:** Prescription with two medications. Confirm?
> **Dentist:** Confirm.
> *(later)*
> **Dentist:** Finish appointment.
> **Assistant:** Printing two documents.

## Who it is for

Dentists who work alone or with one assistant. The first version focuses on a practice in **implant surgery and prosthesis**, which means:

- prescriptions for implant surgery
- try-in and acceptance forms for prostheses

Other specialties are planned for later.

## Key ideas

- **Hands-free is the point.** If the app needs typing or touching a screen during the appointment, it gives no advantage over doing the paperwork on a computer afterwards.
- **The assistant chooses, it does not invent.** The dentist keeps a library of medication protocols, reviewed and accepted by them. A voice request only selects from that library. It is not free dictation, which makes it more reliable and keeps clinical content under the dentist's control.
- **It always knows who is in the chair.** When the dentist calls a patient in, they are marked as "in appointment", and every document goes to that patient. No patient in appointment means no document.
- **Confirm before saving.** The assistant reads back what it understood, and the dentist confirms or corrects.
- **Everything is documented.** Each document is kept with the patient's record and signed by the patient.

## What it is not

- **Not a full clinic management system.** A fuller system with scheduling and patient messages may come much later.
- **Not clinical decision support.** The assistant does not recommend treatments or medications. The dentist is responsible for everything in the library.
- **Not a replacement for professional judgment** or for the legal requirements that apply to prescriptions and signatures.

## Where the project stands

The project is in the design phase. The rules the app is planned to follow are collected in [Business rules](02-business-rules.md). More pages will follow: how the dentist uses the app step by step, the data model, and the roadmap.
