# 📩 Google Form Automation with Email Trigger

## 🚀 Project Overview

This project demonstrates an automated workflow using Google ecosystem tools where user data is collected through a form, stored in a spreadsheet, and triggers real-time email notifications based on user interaction.

---

## 🧩 Tools Used

* Google Forms
* Google Sheets
* Google Apps Script

---

## 🔄 Workflow

1. User fills out Google Form
2. Data is stored in Google Sheets
3. Admin selects checkbox ("Order Placed")
4. Email is automatically sent to the user
5. Status column updates to "Sent"

---

## ⚙️ Features

* Real-time email automation using onEdit trigger
* Custom HTML email templates
* Status tracking to prevent duplicate emails
* Fully automated pipeline (no manual intervention)

---

## 📊 Sheet Structure

| Column | Name                    |
| ------ | ----------------------- |
| A      | Timestamp               |
| B      | Full Name               |
| C      | Phone Number            |
| D      | Email Id                |
| E      | Address                 |
| F      | Status                  |
| G      | Order Placed (Checkbox) |

---

## 💻 Apps Script Code

```javascript
function onEdit(e) {
  var sheet = e.source.getActiveSheet();
  var range = e.range;

  if (range.getColumn() == 7) {

    var row = range.getRow();

    var name = sheet.getRange(row, 2).getValue();
    var email = sheet.getRange(row, 4).getValue();
    var status = sheet.getRange(row, 6).getValue();
    var checkbox = sheet.getRange(row, 7).getValue();

    if (!email) return;

    if (checkbox === true && status !== "Sent") {

      var subject = "Order Place Approved ✅";

      var message = `
        <h2>Hello ${name}</h2>
        <p>Your Order Place has been <b style="color:green;">approved</b> ✅</p>
        <p>We will contact you soon.</p>
        <br>
        <p>Regards,<br>Team</p>
      `;

      GmailApp.sendEmail(email, subject, "", {
        htmlBody: message
      });

      sheet.getRange(row, 6).setValue("Sent");
    }
  }
}
```

---

## 🔔 Trigger Setup

* Go to Apps Script → Triggers
* Add Trigger:

  * Function: onEdit
  * Event Source: From spreadsheet
  * Event Type: On edit

---

## 🎯 Use Cases

* Order confirmation system
* Approval workflow
* Lead management automation
* HR form processing

---

## 📌 Key Highlights

* Built using event-driven architecture
* Eliminates manual email sending
* Improves operational efficiency
* Scalable and easy to customize

---

## 👨‍💻 Author

Vinay Yadav
