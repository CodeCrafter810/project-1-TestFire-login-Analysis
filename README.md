# Project 1: TestFire Login Analysis & Security Assessment

A detailed cybersecurity analysis and documentation of the HTTP request/response workflow, authentication parameters, and session management lifecycle on Altoro Mutual (`testfire.net`).

---

## 📋 Overview

This repository contains a step-by-step security assessment of the authentication mechanism on **Altoro Mutual** (`testfire.net`), a vulnerable web application maintained for testing and educational purposes. 

Using browser-based inspection tools, this project analyzes the HTTP request/response cycle, parameter exposure during authentication, cookie-based session tracking, and session termination mechanics upon logout.

---

## 🎯 Objectives

* **Traffic Capture:** Intercept and analyze HTTP traffic using Chrome Developer Tools.
* **Parameter Inspection:** Identify payload parameter transmission during credential submission.
* **Session Lifecycle Tracking:** Inspect server-issued session tokens (`JSESSIONID`, `AltoroAccounts`) during active and terminated states.
* **Security Evaluation:** Verify proper session invalidation upon user logout.

---

## 🛠️ Tools & Target Environment

* **Target Application:** `http://testfire.net` (Altoro Mutual)
* **Tools Used:** Chrome Developer Tools (Network Tab, Application / Cookies Tab)
* **Protocol:** HTTP (`POST`, `GET`)

---

## 🔍 Technical Analysis & Key Findings

### 1. Authentication Capture (`POST /doLogin`)
During credential submission, traffic was captured on the `doLogin` endpoint:
* **Request URL:** `http://testfire.net/doLogin`
* **HTTP Method:** `POST`
* **HTTP Status Code:** `302 Found` (Redirection to user dashboard upon authentication)

### 2. Payload Inspection
Examining the **Payload** tab exposed cleartext form parameters sent over the wire:
* `uid`: `jsmith`
* `passw`: `Demo1234`

### 3. Session Identification & Cookie Analysis
Key tokens were identified in the **Application / Cookies** tab:
* **`JSESSIONID`:** Server-generated unique identifier used to track active session state across stateless HTTP requests.
* **`AltoroAccounts`:** Application-specific custom cookie storing account state information.

### 4. Session Termination Verification
* **Pre-Logout:** Active `Set-Cookie` response headers and request cookies maintain state between client and server.
* **Post-Logout:** Triggering the logout function invalidates active session tokens server-side, preventing session reuse or replay attacks.

---

## 📚 Key Cyber Concepts Covered

* **Authentication vs. Authorization:** Verifying user identity (`uid`/`passw`) vs. granting access to restricted endpoints.
* **Stateless HTTP & Sessions:** Utilizing client-side cookies to maintain persistent server-side sessions.
* **Session Hygiene:** Ensuring token invalidation upon user logout to maintain system security.

---

## 📄 Repository Files

* `Cybersecurity_Login_Project_Report.pptx` – Project summary and visual presentation slides.
* `README.md` – Project documentation and repository summary.
* `project-1-TestFire-login-analysis.md` – In-depth lab analysis and detailed technical notes.
