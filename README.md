# ✈️ Skyscanner Flight Price Tracker & Analyzer (RPA)

![UiPath](https://img.shields.io/badge/UiPath-2022.10%2B-orange?style=for-the-badge&logo=uipath&logoColor=white)
![REFramework](https://img.shields.io/badge/Architecture-REFramework-blue?style=for-the-badge)
![Language](https://img.shields.io/badge/Language-VB.NET-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge)

> **An enterprise-grade Robotic Process Automation (RPA) solution built with UiPath REFramework to automate flight search, price extraction, and comparative analysis.**

---

## 📖 Overview

The **Skyscanner Flight Analyzer** is designed to eliminate the manual effort of searching for the best flight deals. Utilizing the **Dispatcher & Performer** architecture, this robot reads flight requests from emails, scrapes real-time data from Skyscanner, calculates key metrics (Cheapest, Fastest, Best Value), and delivers a comprehensive HTML report to the user.

### 🎯 Key Goals
* **Automate** repetitive flight search queries.
* **Analyze** multiple airlines and routes instantly.
* **Report** actionable insights via professional HTML emails.

---

## ⚙️ Architecture & Design

This project follows the **Robotic Enterprise Framework (REFramework)** standards, ensuring scalability, robust error handling, and transaction logging.

### 🏗️ Dispatcher (Loader)
1.  **Trigger:** Monitors Outlook for emails with the subject `Flight Request`.
2.  **Validate:** Checks input format (Origin, Destination, Date).
3.  **Queue:** Uploads valid requests to **UiPath Orchestrator Queue**.

### 🤖 Performer (Processor)
1.  **Fetch:** Gets transaction items from the Queue.
2.  **Process:**
    * Navigates to **Skyscanner**.
    * Handles dynamic selectors and "Anti-bot" pop-ups.
    * Extracts data: *Price, Airline, Duration, Stops*.
3.  **Logic:** Calculates **Min/Avg/Max** prices and identifies the best flight.
4.  **Report:** Generates an HTML summary and attaches an Excel report.

---

## 🚀 Key Features

| Feature | Description |
| :--- | :--- |
| **Advanced Scraping** | Handles complex HTML tables and extracts data even when text is missing (using `alt` attributes). |
| **Smart Cleaning** | Uses **Regex** to clean currency symbols and format numbers based on `CultureInfo`. |
| **Dynamic Reporting** | Sends a visually appealing HTML email dashboard with a summary of the analysis. |
| **Error Resilience** | Built-in **Retry Mechanism** for system exceptions (e.g., Browser timeout). |
| **Configurable** | All settings (URLs, Mail Subjects, Queues) are managed via `Config.xlsx`. |

---

## 🛠️ Prerequisites

Before running the robot, ensure you have the following installed:

* **UiPath Studio** (v2021.10 or higher)
* **Google Chrome** (with UiPath Extension enabled)
* **Microsoft Excel**
* **Microsoft Outlook** (Desktop App)

---

## 📦 Installation & Setup

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/YourUsername/Skyscanner-RPA-Bot.git](https://github.com/YourUsername/Skyscanner-RPA-Bot.git)
    ```

2.  **Configure `Data/Config.xlsx`**
    * `OrchestratorQueueName`: Name of your queue (e.g., `SkyscannerQueue`).
    * `MailSubject`: Subject line to filter emails (e.g., `Flight Request`).
    * `MailTo`: Default receiver email.

3.  **Setup Orchestrator**
    * Create a new Queue named **SkyscannerQueue** in UiPath Orchestrator.

4.  **Run the Process**
    * Open `Main.xaml` in UiPath Studio and click **Run**.

---

## 📊 Workflow Structure

The project is modularized for easy maintenance:

* 📂 **Framework**
    * `InitAllSettings.xaml` - Loads configuration.
    * `GetTransactionData.xaml` - Fetches queue items.
* 📂 **Workflows**
    * `Dispatcher.xaml` - Reads Outlook & Uploads to Queue.
    * `Search_Flight.xaml` - Interacts with Skyscanner UI.
    * `Scrape_Flight_Data.xaml` - Extracts structured data.
    * `CalculateMetrics.xaml` - Business logic & Math.
    * `SendFinalReport.xaml` - HTML generation & Emailing.

---

## 📈 Sample Email Report

When the process finishes, the user receives an email formatted as follows:

> **Subject:** Flight Analysis Report - 12.02.2026
>
> **Hello,**
>
> The robot has completed the analysis for **BAKU (GYD) ➡️ LONDON (LHR)**.
>
> | Metric | Details |
> | :--- | :--- |
> | **Cheapest Option** | **$120** (Wizz Air) |
> | **Fastest Option** | **5h 30m** (AZAL) |
> | **Average Price** | $185 |
>
> *Please find the detailed Excel report attached.*

---

## 👨‍💻 Developer

**Murad Balazada**
*RPA Developer & Software Engineer*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/murad-balazada-370256220/)

---

### ⚠️ Disclaimer
*This project is for educational and portfolio purposes only. Web scraping logic relies on the structure of Skyscanner, which may change over time. Please respect the website's `robots.txt` and Terms of Service.*
