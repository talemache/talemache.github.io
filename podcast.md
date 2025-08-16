---
layout: page
title: 
permalink: /podcast/
---

This is my attempt at working through life, creativity, and everything in between. Listen to it here, or on your favorite pod listening app.

<div class="podcast-intro">
  <p>![Ryan Wears a Hat](/assets/img/cat.gif)</p>
</div>

## Recent Episodes

<div id="podcast-episodes" class="podcast-episodes">
  <div class="loading">Loading episodes...</div>
</div>

<div class="podcast-subscribe">
  <h3>Subscribe & Listen</h3>
  <div class="subscribe-links">
    <a href="https://media.rss.com/ryan-wears-a-hat/feed.xml" class="subscribe-btn rss" target="_blank">RSS Feed</a>
    <a href="#" class="subscribe-btn apple" target="_blank">Apple Podcasts</a>
    <a href="#" class="subscribe-btn spotify" target="_blank">Spotify</a>
    <a href="#" class="subscribe-btn google" target="_blank">Google Podcasts</a>
  </div>
</div>

<script>
// Replace with your actual RSS feed URL
const RSS_FEED_URL = 'https://media.rss.com/ryan-wears-a-hat/feed.xml';

async function loadPodcastEpisodes() {
  try {
    // Use a CORS proxy for RSS feeds (or serve from your own domain)
    const proxyUrl = `https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(RSS_FEED_URL)}`;
    
    const response = await fetch(proxyUrl);
    const data = await response.json();
    
    if (data.status === 'ok' && data.items) {
      displayEpisodes(data.items);
    } else {
      showError('Unable to load episodes at the moment.');
    }
  } catch (error) {
    console.error('Error loading podcast episodes:', error);
    showError('Unable to load episodes at the moment.');
  }
}

function displayEpisodes(episodes) {
  const container = document.getElementById('podcast-episodes');
  
  if (episodes.length === 0) {
    container.innerHTML = '<p class="no-episodes">No episodes available yet. Check back soon!</p>';
    return;
  }
  
  const episodesHTML = episodes.map((episode, index) => {
    const pubDate = new Date(episode.pubDate);
    const formattedDate = pubDate.toLocaleDateString('en-US', {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    });
    
    // Extract audio URL from enclosure if available
    const audioUrl = episode.enclosure?.link || '';
    
    // Clean up description (remove HTML tags)
    const description = episode.description?.replace(/<[^>]*>/g, '').substring(0, 200) + '...';
    
    return `
      <div class="episode">
        <div class="episode-header">
          <h3 class="episode-title">
            <a href="${episode.link}" target="_blank">${episode.title}</a>
          </h3>
          <p class="episode-date">${formattedDate}</p>
        </div>
        
        ${audioUrl ? `
          <div class="episode-player">
            <audio controls preload="none">
              <source src="${audioUrl}" type="audio/mpeg">
              Your browser does not support the audio element.
            </audio>
          </div>
        ` : ''}
        
        <div class="episode-description">
          <p>${description}</p>
        </div>
        
        <div class="episode-actions">
          <a href="${episode.link}" class="episode-link" target="_blank">View Full Episode</a>
        </div>
      </div>
    `;
  }).join('');
  
  container.innerHTML = episodesHTML;
}

function showError(message) {
  const container = document.getElementById('podcast-episodes');
  container.innerHTML = `
    <div class="error-message">
      <p>${message}</p>
      <p>In the meantime, you can find episodes on your favorite podcast platform using the links below.</p>
    </div>
  `;
}

// Load episodes when page loads
document.addEventListener('DOMContentLoaded', loadPodcastEpisodes);
</script>

<style>
.podcast-intro {
  background: var(--background-secondary, #f8f9fa);
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid var(--accent-color, #268bd2);
}

.podcast-episodes {
  margin: 2rem 0;
}

.episode {
  background: var(--background-color, #fff);
  border: 1px solid var(--border-color, #eee);
  border-radius: 8px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  transition: box-shadow 0.2s ease;
}

.episode:hover {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.episode-header {
  margin-bottom: 1rem;
}

.episode-title {
  margin: 0 0 0.5rem 0;
  font-size: 1.25rem;
  font-weight: 600;
}

.episode-title a {
  text-decoration: none;
  color: var(--text-color, #333);
}

.episode-title a:hover {
  color: var(--accent-color, #268bd2);
}

.episode-date {
  color: var(--muted-color, #666);
  font-size: 0.9rem;
  margin: 0;
}

.episode-player {
  margin: 1rem 0;
}

.episode-player audio {
  width: 100%;
  max-width: 400px;
}

.episode-description {
  margin: 1rem 0;
  color: var(--text-color, #555);
  line-height: 1.6;
}

.episode-actions {
  margin-top: 1rem;
}

.episode-link {
  color: var(--accent-color, #268bd2);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
}

.episode-link:hover {
  text-decoration: underline;
}

.podcast-subscribe {
  background: var(--background-secondary, #f8f9fa);
  padding: 2rem;
  border-radius: 8px;
  margin: 3rem 0;
  text-align: center;
}

.subscribe-links {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-top: 1rem;
}

.subscribe-btn {
  display: inline-block;
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  transition: transform 0.2s ease;
}

.subscribe-btn:hover {
  transform: translateY(-1px);
  text-decoration: none;
}

.subscribe-btn.rss {
  background: #ff6600;
  color: white;
}

.subscribe-btn.apple {
  background: #000;
  color: white;
}

.subscribe-btn.spotify {
  background: #1db954;
  color: white;
}

.subscribe-btn.google {
  background: #4285f4;
  color: white;
}

.loading, .error-message {
  text-align: center;
  padding: 2rem;
  color: var(--muted-color, #666);
}

.no-episodes {
  text-align: center;
  padding: 2rem;
  color: var(--muted-color, #666);
  font-style: italic;
}

/* Dark mode support */
[data-theme="dark"] .podcast-intro {
  background: var(--background-secondary, #1a1a1a);
}

[data-theme="dark"] .episode {
  background: var(--background-color, #1a1a1a);
  border-color: var(--border-color, #333);
}

[data-theme="dark"] .podcast-subscribe {
  background: var(--background-secondary, #1a1a1a);
}

@media (max-width: 768px) {
  .subscribe-links {
    flex-direction: column;
    align-items: center;
  }
  
  .subscribe-btn {
    width: 200px;
  }
  
  .episode-player audio {
    width: 100%;
  }
}
</style>