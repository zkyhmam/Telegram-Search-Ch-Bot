# 索 Advanced Telegram Search & Indexing Bot 🤖

[![Python Version](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Telegram Group](https://img.shields.io/badge/Support%20Chat-Ask%20Here-blue?logo=telegram)](https://t.me/Zaky1million) <!-- Optional: Link to a support group if you have one -->

<p align="center">
  <img src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExNWg1ajNkeHdzMW5kbjU2dWw0djVnMm5wYmhqamJ3bWZ0eHJzMnAyMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/DSPLv3t6q3j0c/giphy.gif" alt="Bot Animation" width="300"/>
</p>

**An intelligent Telegram bot designed to create a powerful local search engine for your monitored channels, accessible directly within your designated groups.**

This bot leverages the power of **Telethon** (for user account actions like reading channel history) and **python-telegram-bot (PTB)** (for the bot interface and command handling) to provide a seamless experience. It indexes messages locally in an **SQLite** database, ensuring fast and private searches without relying on external services.

---

## ✨ Key Features

*   **🚀 Local Indexing:** Indexes messages from multiple specified public or private channels using a user account session (Telethon).
*   **⚡ Fast Search:** Performs quick searches across the indexed messages directly from allowed Telegram groups.
*   **🔐 Privacy Focused:** All indexed data is stored locally in an SQLite database file.
*   **👑 Admin Control Panel:** Comprehensive inline menu for the admin to:
    *   📊 View Bot Status (Connectivity, Indexing progress)
    *   📈 View Usage Statistics (Total requests, top users, top queries)
    *   📢 Manage Monitored Channels (Add, Remove, List, Refresh Index)
    *   👥 Manage Allowed Groups (Add, Remove, List)
    *   🚫 Manage Excluded Keywords (Add, Remove, List words to ignore during search)
    *   📜 List Own Telegram Chats (Public/Private Channels, Groups)
*   **🤖 Automated Channel Updates:** Automatically indexes new messages posted in monitored channels. *(Requires Handler Setup)*
*   **⚙️ Smart Query Filtering:** Automatically removes common stop words (configurable), dates (YYYY format like 2023, ١٩٩٩), links, and common punctuation before searching.
*   **📈 Statistics Tracking:** Logs search requests, user activity, and query popularity in the local database.
*   **🔄 Index Refresh:** Admins can trigger a manual re-indexing/refresh for all monitored channels.

---

## 📸 Screenshots / Demo

*(**ملاحظة:** قم بإضافة صور GIF أو لقطات شاشة هنا لواجهة البوت، مثل القائمة الرئيسية، نتائج البحث، قائمة الإعدادات، إلخ. استبدل الرابط أدناه)*

<p align="center">
  <img src="link_to_your_screenshot_or_gif.gif" alt="Bot Demo" width="600"/>
</p>

---

## 🛠️ Technology Stack

*   **Python 3.9+**
*   **python-telegram-bot (PTB)**: For the main bot framework and interactions.
*   **Telethon**: For user account interactions (reading channels, getting entities).
*   **SQLite3**: For the local message index database.
*   **Google Generative AI** (Optional): Currently included but not essential for core search functionality.
*   **Asyncio**: For handling asynchronous operations.

---

## 🚀 Setup & Installation

Follow these steps to get the bot up and running:

1.  **Prerequisites:**
    *   Python 3.9 or higher installed.
    *   A Telegram Account (for the user session).
    *   A Telegram Bot Token (get from [@BotFather](https://t.me/BotFather)).
    *   Telegram API ID and API Hash (get from [my.telegram.org](https://my.telegram.org/apps)).

2.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git # استبدل باسم المستخدم واسم المستودع
    cd your-repo-name
    ```

3.  **Install Dependencies:**
    *   **(Recommended)** Create and activate a virtual environment:
        ```bash
        python -m venv venv
        source venv/bin/activate # On Windows use `venv\Scripts\activate`
        ```
    *   Create a `requirements.txt` file with the following content:
        ```txt
        python-telegram-bot[ext]>=20.0 # Check for latest compatible version
        telethon>=1.25 # Check for latest compatible version
        google-generativeai>=0.3 # Or the version you are using
        # Add any other specific libraries if needed
        ```
    *   Install the requirements:
        ```bash
        pip install -r requirements.txt
        ```

4.  **Configuration:**
    *   Open the main Python script (e.g., `test4.py`).
    *   Locate the configuration section near the top.
    *   Fill in your **`API_ID`**, **`API_HASH`**, **`BOT_TOKEN`**, **`ADMIN_ID`** (your Telegram User ID), and **`PHONE_NUMBER`** (international format, e.g., +1234567890).
    *   Optionally, set `ADMIN_USERNAME`.
    *   The bot will create `config.json` for dynamic settings (allowed groups, channels, excluded words) and `channel_index.db` for the database automatically.

5.  **Run the Bot:**
    ```bash
    python test4.py # Or your main script name
    ```

6.  **Telethon Session:** On the first run, Telethon will prompt you in the console to enter your phone number, the code sent to your Telegram account, and potentially your two-step verification password (if enabled). This generates the `user_bot_session.session` file needed for the user account.

---

## 📖 Usage

### Admin Usage

1.  Start a **private chat** with your bot on Telegram.
2.  Send the `/start` command.
3.  The bot will present you with an inline keyboard menu to manage all its features:
    *   **Bot Status:** View connectivity and indexing information.
    *   **Manage Channels:** Add/remove channels for monitoring, list them, refresh the index.
    *   **Manage Groups:** Add/remove groups where users can search, list allowed groups.
    *   **Settings:** Access sub-menus like "Manage Excluded Words".
    *   **Find Movie (Local Index):** Manually search the index as an admin.
    *   **List My Telegram Chats:** Browse channels/groups your user account is in.
    *   **View Statistics:** See usage stats.

### User Usage (in Allowed Groups)

1.  Users (including non-admins) in any group added to the "Allowed Groups" list via the admin panel can use the search.
2.  Simply send a message containing the movie or series name you are looking for (e.g., `Frozen`, `The Matrix 1999`).
3.  The bot will automatically:
    *   Filter the query (remove excluded words, dates, links, punctuation).
    *   Search the local index based on the filtered query.
    *   If results are found, it will reply to the user's message with a formatted list of results (Snippet, Channel, Link).
    *   If no results are found, it will **silently notify the admin** with the user's query details.
    *   If a search error occurs, it will **silently notify the admin**.

---

## 🚫 Excluded Words & Filtering

*   The bot automatically removes common punctuation (`!؟.،;:,\`) and web links from search queries.
*   It also removes 4-digit years starting with 19, 20, ١٩, or ٢٠ (e.g., 1999, 2023).
*   Admins can define a custom list of "stop words" (e.g., "فيلم", "مسلسل", "عايز", "تحميل") via the **Settings -> Manage Excluded Words** menu. These words (case-insensitive) are also removed before searching.
*   This filtering helps improve search accuracy by focusing on the essential keywords.

---

## ✨ Developed By ✨

💻 **Zaky Hamam** 💻

---

## 📞 Contact

Need help or have questions?

<a href="https://t.me/Zaky1million"><img src="https://img.shields.io/badge/Telegram-%40Zaky1million-28A8E9?style=flat&logo=telegram" alt="Telegram"/></a>
<a href="https://wa.me/201280779419"><img src="https://img.shields.io/badge/WhatsApp-%2B201280779419-25D366?style=flat&logo=whatsapp" alt="WhatsApp"/></a>

---

## ©️ License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details (You should create a LICENSE file with the MIT license text).
