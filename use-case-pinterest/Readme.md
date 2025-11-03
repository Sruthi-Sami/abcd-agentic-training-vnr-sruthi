## 🧭 Flow Summary

1. The user provides Pinterest profile data (username, bio, boards, and sample pins).  
2. The system crafts a **humorous, easy-to-read blog** using GPT-4o-mini.  
3. The **Blogger API** publishes the generated blog automatically.

---

## ⚙️ Components and Responsibilities

| Component | Responsibility |
|------------|----------------|
| **OpenAI API** | Generates the blog content from Pinterest data |
| **Google Blogger API** | Publishes the AI-generated blog post to a connected Blogger account |
| **Python Script** | Acts as the orchestrator, handling input parsing, blog creation, and posting |

---

## 🧠 Low-Level Design

### 1️⃣ Input Data Structure

## 🧠 Low-Level Design

---

### 1️⃣ Input Data Structure

```python
profile_data = {
    "username": "DreamyCrafter",
    "bio": "Obsessed with DIYs and aesthetic boards.",
    "boards": [
        {"board_name": "DIY Ideas", "pins": ["Handmade lamps", "Wall decor", "Mini plant pots"]},
        {"board_name": "Dessert Dreams", "pins": ["Chocolate cake", "Strawberry mousse"]}
    ]
}

2️⃣ Blog Generation Logic
The system constructs a detailed prompt using the provided Pinterest data.
It calls the OpenAI API to generate a funny and sarcastic 600–800 word blog.
The generated blog uses subheadings and concludes with a humorous reflection.

python
Copy code
def generate_blog(profile_data):
    # Construct a witty and sarcastic blog using GPT
    ...
3️⃣ Blogger API Integration Flow
mermaid
Copy code
sequenceDiagram
    participant User
    participant Script
    participant BloggerAPI

    User->>Script: Provide Pinterest data
    Script->>BloggerAPI: Authenticate (OAuth 2.0)
    Script->>OpenAI: Generate blog from data
    OpenAI-->>Script: Return witty blog content
    Script->>BloggerAPI: Publish blog post
    BloggerAPI-->>Script: Return post URL
    Script-->>User: Display success + post link
4️⃣ Key API Calls
🔹 OpenAI Blog Generation
python
Copy code
response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": prompt}],
    temperature=0.8,
    max_tokens=1200
)
🔹 Blogger Blog Creation
python
Copy code
post = {
    "title": "Inside the Mind of a Pinterest Dreamer",
    "content": blog_content
}

service.posts().insert(blogId=blog_id, body=post, isDraft=False).execute()
🧩 System Architecture Diagram
mermaid
Copy code
graph LR
    A[User Input (Pinterest Data)] --> B[Python Script]
    B --> C[OpenAI API (Blog Generator)]
    B --> D[Blogger API (Publisher)]
    C --> B
    B --> E[Published Blog on Blogger]
🛠️ Setup Instructions
1️⃣ Install Dependencies
bash
Copy code
pip install openai google-auth google-auth-oauthlib google-api-python-client
2️⃣ Add OpenAI API Key
bash
Copy code
export OPENAI_API_KEY="your_openai_api_key"
3️⃣ Set Up Google OAuth
Go to Google Cloud Console → APIs & Services → Credentials.

Create an OAuth 2.0 Client ID (Desktop App).

Download it as client_secret.json and place it in your project directory.

4️⃣ Run the Script
bash
Copy code
python main.py
On the first run, a browser will open to let you log in to your Google account.
Once authenticated, your Blogger account is linked automatically.

🧭 Example Output
🔸 Input
json
Copy code
{
  "username": "CreativeSoul",
  "bio": "Turning random thoughts into DIY chaos.",
  "boards": ["Home Decor", "Snack Fixes", "Mood Boards"]
}
🔸 Output (Excerpt)
Inside the Mind of a Pinterest Dreamer
You ever pin 500 things and actually do… zero? Same.
My DIY board looks like Martha Stewart and chaos had a baby...

🧾 Summary
Feature	Description
Automation Level	Fully automated blog generation and posting
Tone	Witty, humorous, sarcastic
APIs Used	OpenAI GPT-4o-mini, Google Blogger API
Language	Python
Auth Mechanism	OAuth 2.0
Output	Live blog post published on Blogger

💡 Future Enhancements
✨ Add image embedding from Pinterest pins

📅 Schedule auto-posting

🧠 Support tone customization (e.g., professional, poetic, Gen Z slang)

🌐 Extend to WordPress and Medium APIs

