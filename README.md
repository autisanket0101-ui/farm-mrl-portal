
# Farm MRL Portal

Digital Farm Management Portal for Monitoring Maximum Residue Limits (MRL) in Livestock[cite: 8]. 

## Overview
Unmonitored antimicrobial usage causes drug residues to exceed safe MRL thresholds in animal products like meat, milk, and eggs[cite: 11]. This project provides a digital tool for farm operators to track Antimicrobial Use (AMU) against FSSAI MRL standards[cite: 10]. 

The system replaces manual, error-prone record-keeping by computing real-time residue percentages based on days elapsed since administration, using an exponential residue decay model[cite: 11, 17]. It also features an AI-powered chatbot to guide farmers on regulatory compliance[cite: 10].

## Key Features
* **Time-Aware Residue Model:** Computes real-time MRL status using the formula `Residue(t) = InitialResidue% x e^(decayRate x daysElapsed)`[cite: 17]. 
* **Dynamic Status Tracking:** Automatically color-codes animal status based on FSSAI thresholds: > 10% residue is EXCEEDED (Red), 5%-10% is WARNING (Orange), and < 5% is SAFE (Green)[cite: 17].
* **AI/RAG Compliance Chatbot:** A RAG-powered chatbot answers FSSAI compliance queries in plain language using the FSSAI Compendium VI database and the farmer's own records[cite: 10, 12, 20].
* **Real-Time AI Streaming:** Responses from the GPT model are delivered word-by-word via Server-Sent Events (SSE)[cite: 14, 18].
* **Instant PDF Reporting:** Generates a one-tap Slaughter Readiness PDF report entirely in-browser, listing every animal's compliance status without requiring server uploads[cite: 10, 12, 20].

## Tech Stack
* **Frontend:** React 18, TypeScript, Vite, TailwindCSS[cite: 14].
* **Backend:** Node.js / Express 5[cite: 14].
* **Database & Security:** Supabase (PostgreSQL), pgvector extension, JWT Authentication, and Row Level Security (RLS)[cite: 14, 20].
* **AI & Embeddings:** OpenAI GPT (gpt-5-nano-2025-08-07) and OpenAI text-embedding-3-small (1536-dimensional vectors)[cite: 14, 15, 18].
* **PDF Generation:** @react-pdf/renderer (client-side)[cite: 14, 20].

## AI / RAG Pipeline Architecture
1. The user types a question in the React Chat Widget[cite: 18].
2. The query is converted into a 1536-dimensional vector using text-embedding-3-small [cite: 18].
3. Parallel execution occurs: pgvector  performs a similarity search to fetch the top-5 FSSAI document chunks, while the system fetches the user's specific `drug_usage_logs` via a JWT-scoped Supabase client[cite: 18].
4. The system merges the regulatory context and personal farm records into a prompt for the GPT model[cite: 18].
5. The model streams the response back to the browser in real time[cite: 18].

## Future Enhancements
* **Multi-Standard Toggle:** Support for EU MRL Regulation, FDA/CVM, and Codex Alimentarius[cite: 19].
* **Mobile PWA & IoT:** Offline support for field use and automatic dosage logging from smart dispensers[cite: 19].
* **Real-Time Alerts:** SMS/email notifications when an animal's withdrawal period ends[cite: 19].

---
*Developed by: Sanket Auti, Aditya Grover, Omkar Bankar, Anvay Chimbalkar*[cite: 8]
