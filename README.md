# React + WordPress REST API (Basic Auth) – Post & Media Upload

## 📌 Project Overview

Ye project **React frontend + WordPress REST API backend** use karta hai jisme user **posts create, edit, delete aur media upload** kar sakta hai.

Security ke liye **Basic Authentication plugin** use kiya gaya hai. Iska matlab hai ki bina authentication ke koi bhi user **post create, update ya delete nahi kar sakta**.

Project mainly development aur testing ke purpose se banaya gaya hai.

---

# 🧠 Project Flow

```
React App
   ↓
Send API Request (Authorization Header)
   ↓
WordPress REST API
   ↓
Basic Auth Plugin Authenticate User
   ↓
If Valid → Post / Media Created
If Invalid → 401 Unauthorized
```

---

# 📂 Project Structure

```
project-root
│
├── wordpress-plugin
│     └── json-basic-authentication.php
│
├── react-app
│     ├── components
│     │     └── AddPost.jsx
│     │
│     └── API requests (Post + Media Upload)
│
└── README.md
```

---

# 🔐 WordPress Basic Authentication Plugin

Ye plugin WordPress REST API ke liye **Basic Authentication enable karta hai**.

### Plugin Code

```php
Plugin Name: JSON Basic Authentication
```

### 📌 Important

Ye plugin sirf **development purpose** ke liye recommended hai.

Production me better option:

* JWT Authentication
* OAuth Authentication

---

# 🚀 React API Requests

## 1️⃣ Media Upload API

WordPress media API **file directly body me expect karti hai**.

```javascript
const response = await fetch(
  "http://localhost/wordpress/wp-json/wp/v2/media",
  {
    method: "POST",

    headers: {
      // Basic Authentication
      "Authorization": "Basic " + btoa("user:password"), //  "Basic " space required hay ///

      // File name send karna required hota hai
      "Content-Disposition": `attachment; filename="${featuredMediaFile.name}"`,

      // File ka type (image/png, image/jpeg)
      "Content-Type": featuredMediaFile.type
    },

    // File directly body me send hoti hai
    body: featuredMediaFile
  }
);
```

### Response Example

```
{
 id: 123,
 source_url: "http://localhost/wordpress/wp-content/uploads/image.jpg"
}
```

---

# 📝 Create Post API

Post create karne ke liye WordPress REST API endpoint:

```
/wp-json/wp/v2/posts
```

### React Request

```javascript
const response = await fetch(
  "http://localhost/wordpress/wp-json/wp/v2/posts",
  {
    method: "POST",

    headers: {
      "Authorization": "Basic " + btoa("user:password"),

      // JSON body send karne ke liye required
      "Content-Type": "application/json"
    },

    body: JSON.stringify({
      title: AddTitle,
      content: AddContent,
      status: "publish",
      categories: [parseInt(AddCategory)],
      featured_media: featuredMediaId
    })
  }
);
```

---

# 📷 Media Upload Flow

```
1 User selects image
2 React sends image → WordPress Media API
3 WordPress uploads image
4 API returns media ID
5 Media ID used in Post API as featured_media
```

---

# 🛠 Requirements

```
Node.js
React
WordPress
WordPress REST API
Basic Auth Plugin
```

---

# ⚠️ Important Notes

### 1️⃣ Without Authorization

User **post create / edit / delete nahi kar sakta**

```
401 Unauthorized
```

### 2️⃣ Correct Header Required

```
Authorization: Basic base64(username:password)
```

### 3️⃣ Media Upload me File Direct Body me Send Hoti Hai

❌ Wrong

```
FormData
```

✅ Correct

```
body: file
```

---

# 📚 Learning Purpose

Is project se ye concepts samajh aate hain:

* React + WordPress Headless CMS
* WordPress REST API
* Authentication
* Media Upload
* CRUD Operations

---

# 👨‍💻 Author

Developer: **Pranshu Singh**

Technology Stack:

* React
* WordPress
* REST API
* Tailwind CSS
* JavaScript

---
