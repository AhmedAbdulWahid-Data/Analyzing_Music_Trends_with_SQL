# Analyzing Music Trends with SQL 🎵💿

---
**Spotify** has revolutionized the music industry, becoming the go-to platform for streaming millions of tracks worldwide. Understanding how music performs on Spotify is crucial for 🎤 artists, 🎼 producers, and 🎧 industry professionals looking to maximize their reach and engagement.  

<img width="691" alt="Screenshot 2025-03-13 at 2 58 54 PM" src="https://github.com/user-attachments/assets/c00f6821-16bf-47a3-8b2a-1cd9bd30cd91" />  


## 📊 Project Overview  

In this project, we will explore a **Spotify dataset** containing detailed information about 🎶 songs, 📀 albums, 🎸 artists, and their **streaming performance**. Using **SQL**, we will extract key insights such as:  
✅ The most **streamed tracks**  
✅ **Album performance** and trends  
✅ **Engagement metrics** like streams, danceability, energy, and popularity  

## 🔍 Key Objectives  

This project aims to answer **15 key questions**, categorized into **Easy, Medium, and Advanced** levels. These queries will help us analyze:  
🎵 **Track popularity**  
🎤 **Artist performance**  
🎼 **Audio features** influencing success on **Spotify**  

## 🚀 Why This Matters?  

By leveraging **SQL**, we can efficiently analyze **millions** of music records and uncover patterns that drive the streaming industry. This project is **not just about querying data**—it’s about making **data-driven decisions** that can help **artists, producers, and music executives** understand:  
📈 **Audience preferences**  
🔝 **Market trends**  
💡 **Key factors influencing success**  

Let’s dive into the **data-driven world of music streaming!** 🎶📊  

---
## 🎵 Spotify Music Analysis Project  

You can download the dataset here: [Spotify Dataset](https://www.kaggle.com/datasets/sanjanchaudhari/spotify-dataset) 📥  

### 📌 Step 1: Creating the Table  

Before analyzing the data, we first create the `spotify` table to store detailed information about songs, albums, artists, and streaming performance.

```sql
-- Drop table if it exists
DROP TABLE IF EXISTS spotify;

-- Create table
CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);


