# KinWell

Automated phone call check-ins for elderly loved ones.
No extra hardware required. Get peace-of-mind with real-time reports.
**Stay connected with your loved ones**

[link to private repo](https://github.com/kinwellkrew/kinwell)

---

## Summary

* KinWell is a wellness-check platform that uses automated phone workflows to verify the safety of elderly family members.
* The technical focus of this project was building a full-stack application with a relational database backend (Supabase)—including schema design, relational modeling, secure access policies, and real-time event logging.

---

## Technologies

* **Next.js** (full-stack TypeScript) + Tailwind/shadcn UI
* **Supabase** (Postgres + Auth)
* **Scheduled Edge Functions** to automate calls
* **Twilio** for phone number and calling
* **ElevenLabs** for AI voice + call summary generation
* **Stripe** for subscriptions

---

## What I Learned

* How to design and normalize a real production-grade relational schema

  * Getting started teaches you more than staring at a whiteboard
* How to implement Row-Level Security (RLS) and fine-grained access controls
* How to reason about and optimize queries involving scheduling and event workflows

---

## ERD

*(ERD diagrams shown in the slideshow; two versions: initial schema → improved schema)*

---

## Goals & Timeline

* **Public MVP with subscriptions in 1–2 months**

  * Scheduled Edge Functions (polling)
  * Improvements to data relationships for scaling
  * Stripe integration for subscriptions
  * Migrate to a cheaper AI/Agent platform (ElevenLabs is expensive)
* **Explore hardware integrations**

---

## Demo

*(Slide shows UI examples of KinWell dashboard and check-in feed.)*

---

## AI Integrations (Current)

* **AI-generated caller voice:** Text-to-speech generates warm, natural-sounding check-ins.
* **AI-generated call summaries:** Each call transcript is summarized using LLMs so caregivers can immediately understand outcomes without reading the entire conversation.

**Today:** AI enhances communication clarity and user experience—not decision-making.

---

## Future AI Plans

We plan to expand KinWell beyond detecting missed calls. Upcoming AI capabilities include:

* **Distress detection:** Detect confusion, stress, or medical concern using transcript and vocal cues.
* **Semantic intent classification:** Determine whether the user is actually “okay,” even if responses are indirect or ambiguous.
* **Personalized call scripts:** Adapt tone/questions based on prior behavior or health conditions.
* **Risk scoring:** Flag patterns that suggest deterioration or increased risk.

AI will act as an intelligent support layer that augments caregivers—not replaces them.

---

## How AI Assisted in Building the Project

* Used AI (ChatGPT) to refine the database schema, RLS policies, and table relationships.
* Used AI to draft/revise SQL queries, indexing approaches, and trigger logic.
* Used AI to generate synthetic test data for validating workflows.
* Used AI as a sounding board for architecture design and reasoning about edge cases.

---

## Failover Strategy

* Calls are made and logged independently so partial failures never corrupt workflow state—each call uses a webhook, i.e., a new, idempotent connection.
* The compute layer **does not rely on in-memory state** (Supabase Edge Functions). If an instance crashes:

  * No check-in workflow is lost
  * No state is corrupted
  * No long-lived connections are dropped
  * A fresh instance simply handles the next event

This makes the system inherently fault-tolerant.

---

## Why KinWell Is Interesting to Me

* KinWell is personally meaningful—a solution inspired by real needs in my family.
* Pairing that motivation with a technically challenging backend allowed me to build something impactful while applying everything learned about relational modeling, constraints, and scalable data systems.

---

## The End

[https://kinwellcare.vercel.app/](https://kinwellcare.vercel.app/)
