Pinterest-to-Blogger AI Blog Generator
📘 Overview

This project automatically generates witty, funny, and sarcastic blog posts based on Pinterest profile data, and publishes them directly to Blogger using the Blogger API. It integrates OpenAI’s GPT model for blog generation and Google’s Blogger API for posting automation.

🚀 High-Level Architecture
flowchart TD
    A[User Inputs Pinterest Data] --> B[Blog Generator (OpenAI API)]
    B --> C[Generated Blog Content]
    C --> D[Blogger API Integration]
    D --> E[Published Blog Post on Blogger]


Flow Summary:

The user provides Pinterest profile data (username, bio, boards, and sample pins).

The system crafts a humorous, easy-to-read blog using GPT-4o-mini.

The Blogger API publishes the generated blog automatically.

⚙️ Components and Responsibilities
Component	Responsibility
OpenAI API	Generates the blog content from Pinterest data.
Google Blogger API	Publishes the AI-generated blog post to a connected Blogger account.
Python Script	Acts as the orchestrator, handling input parsing, blog creation, and posting.
🧠 Low-Level Design
1️⃣ Input Data Structure
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

Function:

def generate_blog(profile_data):
    ...

3️⃣ Blogger API Integration Flow
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
response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": prompt}],
    temperature=0.8,
    max_tokens=1200
)

🔹 Blogger Blog Creation
post = {
    "title": "Inside the Mind of a Pinterest Dreamer",
    "content": blog_content
}
service.posts().insert(blogId=blog_id, body=post, isDraft=False).execute()

🧩 System Architecture Diagram
graph LR
    A[User Input (Pinterest Data)] --> B[Python Script]
    B --> C[OpenAI API (Blog Generator)]
    B --> D[Blogger API (Publisher)]
    C --> B
    B --> E[Published Blog on Blogger]

🛠️ Setup Instructions

Install Dependencies

pip install openai google-auth google-auth-oauthlib google-api-python-client


Add OpenAI API Key

export OPENAI_API_KEY="your_openai_api_key"


Set Up Google OAuth

Go to Google Cloud Console → APIs & Services → Credentials.

Create an OAuth 2.0 Client ID (Desktop App).

Download it as client_secret.json.

Run the Script

python main.py


Authenticate Once

A browser will open to let you log in to your Google account.

After that, your Blogger is linked.

🧭 Example Output

Input:

username: "CreativeSoul"
bio: "Turning random thoughts into DIY chaos."
boards: [“Home Decor”, “Snack Fixes”, “Mood Boards”]


Output (Excerpt):

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