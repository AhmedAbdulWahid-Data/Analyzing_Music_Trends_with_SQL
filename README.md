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

# You can download the dataset here: [Spotify Dataset](https://www.kaggle.com/datasets/sanjanchaudhari/spotify-dataset) 📥  

## 📌 Creating the Table  

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
```

---

# 📌 15 SQL Practice Questions  

---

## 🟢 Easy Level  

### 1. Retrieve the names of all tracks that have more than **1 billion** streams.  

```sql
SELECT track 
FROM spotify 
WHERE stream > 1000000000;
```


### 2. List all **albums** along with their respective **artists**.

```sql
SELECT DISTINCT album, artist 
FROM spotify;
```


### 3. Get the **total number of comments** for tracks where `licensed = TRUE`.  

```sql
SELECT SUM(comments) AS total_comments 
FROM spotify 
WHERE licensed = TRUE;
```


### 4. Find all **tracks** that belong to the album type **'Single'**.  

```sql
SELECT track 
FROM spotify 
WHERE album_type = 'Single';
```


### 5. Count the **total number of tracks** by each **artist**. 

```sql
SELECT artist, COUNT(track) AS total_tracks 
FROM spotify 
GROUP BY artist;
```


---

## 🔵 Medium Level

### 6. Calculate the average danceability of tracks in each album.

```sql
SELECT album, AVG(danceability) AS avg_danceability 
FROM spotify 
GROUP BY 1
ORDER BY 2 DESC;
```


### 7. Find the top 5 tracks with the highest energy values.

```sql
SELECT track, energy 
FROM spotify 
ORDER BY energy DESC 
LIMIT 5;
```


### 8. List all tracks along with their views and likes where official_video = TRUE.

```sql
SELECT track, views, likes 
FROM spotify 
WHERE official_video = TRUE;
```


### 9. For each album, calculate the total views of all associated tracks.

```sql
SELECT album, SUM(views) AS total_views 
FROM spotify 
GROUP BY album;
```


### 10. Retrieve the track names that have been streamed on Spotify more than YouTube views.

```sql
SELECT track
FROM spotify
GROUP BY track
HAVING 
    COALESCE(SUM(CASE WHEN most_played_on = 'Spotify' THEN stream END), 0) 
    > COALESCE(SUM(CASE WHEN most_played_on = 'Youtube' THEN stream END), 0);
```


---

## 🔴 Advanced Level

### 11. Find the top 3 most-viewed tracks for each artist using window functions.

```sql
WITH ranked_tracks
AS
(
SELECT artist,
       track,
       SUM(views) AS Total_views, 
       DENSE_RANK() OVER (PARTITION BY artist ORDER BY SUM(views) DESC) AS rank 
FROM spotify
GROUP BY 1, 2
ORDER BY 1, 3 DESC
)
SELECT * FROM ranked_tracks
WHERE rank <= 3;
```


### 12. Write a query to find tracks where the liveness score is above the average.

```sql
SELECT track, liveness 
FROM spotify 
WHERE liveness > (SELECT AVG(liveness) FROM spotify);
```


### 13. Use a WITH clause to calculate the difference between the highest and lowest energy values for tracks in each album.

```sql
WITH energy_stats AS (
    SELECT album, 
           MAX(energy) AS max_energy, 
           MIN(energy) AS min_energy 
    FROM spotify 
    GROUP BY album
)
SELECT album, (max_energy - min_energy) AS energy_difference 
FROM energy_stats;
```


### 14. Find tracks where the energy-to-liveness ratio is greater than 1.2.

```sql
SELECT track, energy, liveness, (energy / liveness) AS ratio 
FROM spotify 
WHERE (energy / liveness) > 1.2;
```


### 15. Calculate the cumulative sum of likes for tracks ordered by the number of views using window functions.

```sql
SELECT track, views, likes, 
       SUM(COALESCE(likes, 0)) OVER (ORDER BY views ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cumulative_likes
FROM spotify;
```


---

# 🎶 Final Thoughts

### By answering these 15 key SQL questions, we can uncover valuable music trends on Spotify. This project isn’t just about practicing SQL—it’s about understanding data-driven insights in the music streaming industry. 🎵📊


# If you’re serious about becoming a data genius 😎 
# 👉 [Follow me on LinkedIn](https://www.linkedin.com/in/ahmed-abdulwahid/) 
    
