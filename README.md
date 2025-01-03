# Spotify Analytics Dashboard

## 📊 Project Overview
The **Spotify Analytics Dashboard** is an advanced Power BI dashboard designed to provide detailed insights into song performance, user engagement metrics, and streaming trends. With features like custom visuals using Deneb, dynamic HTML integration, and data modeling through Bravo, this dashboard enables stakeholders to make data-driven decisions in music marketing and playlist curation.

---

## 🎯 Objectives and Key Performance Indicators (KPIs)

### **Objectives**
- **Monitor Song Performance**: Track streams, engagement metrics, and top-performing tracks.
- **Analyze Trends**: Identify patterns in streaming behavior over time and by audience preferences.
- **Support Decision-Making**: Provide actionable insights for playlist curation, artist promotion, and marketing campaigns.

---

### **Key Performance Indicators (KPIs)**
1. **Total Streams**:
   - Tracks the total number of streams for individual tracks.
   - **Example**: *Blinding Lights* by The Weeknd has 4bn streams.

2. **Top Songs vs. Average Streams**:
   - Compares the performance of the top track against the average streams for all tracks.
   - **Example**: *Blinding Lights* outperformed the average by 620.4%.

3. **Engagement Metrics**:
   - **Energy %**: Indicates the intensity and activity level of a track (e.g., workout music).
   - **Danceability %**: Highlights tracks suitable for dancing.
   - **Valence %**: Reflects the positivity or mood of a song.
   - **Acousticness %, Liveness %, Speechiness %**: Offer deeper insight into a track’s musical characteristics.

4. **Release Trends**:
   - Tracks the number of songs released over time and streaming behavior by day and month.

5. **Playlist Inclusion**:
   - Tracks how many playlists a song is included in (Spotify, Apple Music, Deezer, Shazam).

6. **Visual Identity**:
   - Dynamically displays the album cover of the top-performing track for context and branding.

---

## 🖼️ Visuals Explained

### **1. KPI Cards**
- **Purpose**: Summarize critical metrics for quick decision-making.
- **Metrics**:
  - Track name, artist, release date, and streams.
  - Engagement metrics (e.g., energy %, danceability %, valence %).
  - Top song performance compared to the average.

---

### **2. Heatmap**
- **Purpose**: Visualizes streaming behavior by day and month.
- **Insights**:
  - Fridays have the highest streams, aligning with new music release schedules.
  - May sees peak streaming activity, likely due to seasonal trends.
- **Tools Used**: Created with Deneb using rectangular marks to represent data density.

---

### **3. Bar Chart**
- **Purpose**: Ranks tracks by the total number of streams.
- **Insights**:
  - Highlights top tracks like *About Damn Time*, providing immediate visibility into popular songs.

---

### **4. Line Chart**
- **Purpose**: Analyzes trends in track releases over time.
- **Insights**:
  - Significant growth in releases post-2010, showcasing the rise of streaming platforms.

---

### **5. Circular Gauge**
- **Purpose**: Displays the energy level of the selected track dynamically.
- **Insights**:
  - Example: *Blinding Lights* has a 64% energy rating, making it ideal for upbeat playlists.
- **Tools Used**: Created with Deneb using pie marks and color gradients.

---

### **6. Dynamic Album Cover**
- **Purpose**: Showcases the album art of the most-streamed track dynamically.
- **Insights**:
  - Adds a professional, branded touch to the dashboard.
- **Tools Used**: HTML integration to dynamically render the cover art.

---

## ⚙️ Tools and Integrations

### **1. Bravo for Power BI**
- **Purpose**: To create a Calendar Table for date-based analysis.
- **Steps**:
  1. Load the Spotify dataset into Power BI.
  2. Use Bravo to generate a calendar table.
  3. Join the calendar table with the dataset on the `released_year`, `released_month`, and `released_day` fields.
- **Learn More**: [Bravo for Power BI](https://bravo.bi/)

---

### **2. HTML Integration**
- **Purpose**: Dynamically render the album cover of the top track.
- **Implementation**:
  ```DAX
  _Image_html =
  VAR x =
      CALCULATE(
          MAX('Spotify Dataset'[cover_url]),
          'spotify-2023'[streams] = MAX('spotify-2023'[streams])
      )
  RETURN
      "<!DOCTYPE html>
      <html lang='en'>
      <head>
          <style>
              .image-container {
                  position: relative;
                  width: 470px;
                  height: 144px;
                  overflow: hidden;
                  border-radius: 10px;
              }
              .image-container img {
                  object-fit: cover;
                  width: 100%;
                  height: 100%;
              }
          </style>
      </head>
      <body>
          <div class='image-container'>
              <img src='" & x & "' alt='Album Cover'>
          </div>
      </body>
      </html>"

#### **How It Works**
Dynamically retrieves the album art URL of the top track and renders it in Power BI using an HTML Viewer visual.

---

### **3. Deneb Integration**
Deneb was used to create advanced visuals like the heatmap and circular gauge.

#### **Heatmap Code Example**
```json
{
  "mark": {"type": "rect", "tooltip": true},
  "encoding": {
    "x": {"field": "Month", "type": "ordinal", "axis": {"labelColor": "white"}},
    "y": {"field": "Day of Week", "type": "ordinal", "axis": {"labelColor": "white"}},
    "color": {"field": "_Track", "type": "quantitative", "scale": {"range": ["#0f3c1f", "#1db954", "#b3b3b3"]}}
  }
}
```
#### **Why Deneb?**
1. Provides precise control over visual aesthetics and interactivity.
2. Enables the creation of visuals beyond Power BI’s default options.