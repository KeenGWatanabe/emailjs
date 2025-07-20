Service ID: service_c4i7t9i


If **Boomerang isn't working** for you and you want a **simple JavaScript solution** to schedule and send emails, you can build a basic **HTML/JS frontend** (hosted on GitHub Pages) that triggers emails via a backend service like **EmailJS**, **SendGrid**, or **SMTP.js**.  

Here's a **step-by-step guide** to create a **GitHub Pages app** that schedules emails:

---

## **📨 Option 1: EmailJS (Easiest, No Backend Needed)**
EmailJS lets you send emails directly from JavaScript without a server.

### **1. Set Up EmailJS**
- Sign up at **[EmailJS](https://www.emailjs.com/)**.
- Go to **Email Services** → Connect **Gmail** or another email service.
- Get your:
  - **Service ID**  
  - **Template ID** (create one)  
  - **User ID (Public Key)**  

### **2. HTML/JS Code (GitHub Pages)**
```html
<!DOCTYPE html>
<html>
<head>
  <title>Email Scheduler</title>
  <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3.2.0/dist/email.min.js"></script>
  <script>
    (function() {
      emailjs.init("YOUR_USER_ID"); // Initialize EmailJS
    })();

    function scheduleEmail() {
      const email = document.getElementById("email").value;
      const subject = document.getElementById("subject").value;
      const message = document.getElementById("message").value;
      const delayMinutes = document.getElementById("delay").value;

      // Calculate future time
      const now = new Date();
      const scheduledTime = new Date(now.getTime() + delayMinutes * 60000);

      // Schedule email
      setTimeout(() => {
        emailjs.send("YOUR_SERVICE_ID", "YOUR_TEMPLATE_ID", {
          to_email: email,
          subject: subject,
          message: message
        })
        .then(() => alert("Email sent!"))
        .catch(err => alert("Error: " + err));
      }, delayMinutes * 60000);

      alert(`Email scheduled for ${scheduledTime}`);
    }
  </script>
</head>
<body>
  <h1>Email Scheduler</h1>
  <input type="email" id="email" placeholder="Recipient Email" required><br>
  <input type="text" id="subject" placeholder="Subject" required><br>
  <textarea id="message" placeholder="Message" required></textarea><br>
  <input type="number" id="delay" placeholder="Delay (minutes)" min="1" required><br>
  <button onclick="scheduleEmail()">Schedule Email</button>
</body>
</html>
```
### **3. Host on GitHub Pages**
1. Upload this to a **GitHub repo**.
2. Go to **Settings → Pages** → Enable GitHub Pages.
3. Done! Your app will be live at:  
   `https://[your-username].github.io/[repo-name]/`

---

## **📨 Option 2: SMTP.js (More Control, But Needs a Backend)**
If you want **more control** (but need a backend), use **SMTP.js** with **FormSubmit.co** or **a Node.js server**.

### **1. Simple SMTP.js Example**
```javascript
function sendEmail() {
  Email.send({
    SecureToken: "YOUR_SMTP_TOKEN",
    To: document.getElementById("email").value,
    From: "your-email@gmail.com",
    Subject: document.getElementById("subject").value,
    Body: document.getElementById("message").value
  }).then(() => alert("Email sent!"));
}
```
- Requires an **SMTP provider** (like Elastic Email, SendGrid, or Gmail with App Password).

---

## **🚀 Which One Should You Use?**
| Solution | Pros | Cons |
|----------|------|------|
| **EmailJS** | No backend, easy setup | Limited to 200 emails/month (free) |
| **SMTP.js** | More flexible | Needs SMTP credentials |
| **Node.js + SendGrid** | Full control | Requires backend hosting |

---

### **Final Recommendation**
- **For simplicity** → Use **EmailJS** (GitHub Pages-friendly).  
- **For more emails** → Use **SMTP.js + FormSubmit.co**.  
- **For full automation** → Use **Node.js + Cron jobs** (requires Heroku/Glitch).  

Would you like help setting up a **Node.js backend** for more advanced scheduling? 🚀