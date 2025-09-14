# Project Foothills: A Tumblr Poetry Blog Theme Specification
*For bkpoetry.com - Kenny Brown's Writer Portfolio*

## Core Philosophy & Design Ethos

**PRIMARY GOAL**: Create an authentic digital space that feels like Kenny's creative workshop—where emerging writers feel welcomed into a community, not pitched to by a consultant.

### Design Principles
- **Community Over Commerce**: This is a gathering place for writers, not a corporate service provider
- **Accessible Activism**: Reflect Kenny's commitment to marginalized voices and accessibility advocacy
- **Queer & Indigenous Aesthetics**: Draw from authentic cultural aesthetics rather than mainstream corporate design
- **Calgary Creative Scene**: Should feel connected to the local Alberta arts community
- **Tumblr-Native Warmth**: Embrace the platform's culture of authentic personal expression

---

## Visual Design Direction

### Color Palette
- **Primary**: Prairie earth tones—think autumn aspens, chinook skies, foothills at sunset
- **Accent**: Muted jewel tones that nod to beadwork and textile traditions
- **Background**: Warm off-white, like aged manuscript paper
- **Text**: Deep charcoal with warm undertones, never harsh black
- **Links**: Earthy burnt orange that shifts to deep teal on hover
- **Queer Pride Subtle Nods**: Incorporate pride flag colors as subtle accent elements

### Typography
- **Headers**: A slightly irregular serif that feels hand-lettered (thinking zine aesthetic)
- **Poetry**: Elevated serif with excellent line spacing for breath and pause
- **Body Text**: Highly readable serif that works for long-form reading
- **UI Elements**: Clean, accessible sans-serif
- **Hierarchy**: Gentle but clear, using spacing and subtle weight changes

### Visual Style
- **Borders**: Organic, hand-drawn feeling lines
- **Spacing**: Generous breathing room—let the poetry breathe
- **Images**: Film grain textures, indie press aesthetics, zine-inspired elements
- **Shadows**: Soft, warm shadows that suggest candlelight or reading lamp glow
- **Interactive Elements**: Subtle animations that feel organic, not corporate

---

## Technical Implementation (Tumblr Variables)

### Required Custom Variables
```html
<!-- Custom Meta Variables for Theme Options -->
<meta name="text:Calendly Link" content=""/>
<meta name="text:Substack Embed Code" content=""/>
<meta name="text:Email Address" content="mail@brennanbrown.ca"/>
<meta name="text:Write Club Description" content=""/>
<meta name="text:Current Reading" content=""/>
<meta name="text:Instagram Handle" content=""/>
<meta name="text:Twitter Handle" content=""/>

<!-- Blogroll Links -->
<meta name="text:Blogroll Link 1 URL" content=""/>
<meta name="text:Blogroll Link 1 Title" content=""/>
<meta name="text:Blogroll Link 1 Description" content=""/>
[...repeat for 8-10 blogroll entries]

<!-- Custom Colors -->
<meta name="color:Accent Color" content="#D2691E"/>
<meta name="color:Link Color" content="#B8860B"/>
<meta name="color:Background" content="#FFFEF7"/>
<meta name="color:Text" content="#2F2F2F"/>

<!-- Custom Options -->
<meta name="if:Show Calendly CTA" content="1"/>
<meta name="if:Show Current Reading" content="1"/>
<meta name="if:Enable Poetry Special Formatting" content="1"/>
```

### Header Structure
```html
<header class="site-header sticky">
  <div class="header-content">
    <h1 class="site-title"><a href="/">{Title}</a></h1>
    <nav class="main-nav">
      <a href="/about">About</a>
      <a href="/books">Books</a>
      <a href="/contact">Contact</a>
      {block:AskEnabled}<a href="/ask">{AskLabel}</a>{/block:AskEnabled}
      {block:SubmissionsEnabled}<a href="/submit">{SubmitLabel}</a>{/block:SubmissionsEnabled}
      <a href="/random">Random</a>
      <a href="/archive">Archive</a>
    </nav>
  </div>
</header>
```

### Hero Section (Homepage Only)
```html
{block:IndexPage}
<section class="hero-section">
  <div class="hero-content">
    <h2 class="hero-greeting">Hey there! I'm Kenny.</h2>
    <p class="hero-intro">
      I believe every voice deserves to be heard—especially the ones that have been overlooked. 
      As the founder of Write Club, I work with emerging writers to find their truth and power through storytelling.
    </p>
    {block:IfShowCalendlyCTA}
      <div class="cta-container">
        <p class="cta-text">Working on something and need a writing buddy?</p>
        <a href="{text:Calendly Link}" class="cta-button">Let's chat over decaf ☕</a>
      </div>
    {/block:IfShowCalendlyCTA}
  </div>
</section>
{/block:IndexPage}
```

---

## Layout Structure

### Main Content Area
```html
<div class="content-wrapper">
  <main class="posts-container">
    {block:Posts}
      <article class="post {PostType}" data-post-id="{PostID}">
        <!-- NPF & Text Posts with Poetry Detection -->
        {block:Text}
          <div class="post-content text-post">
            {block:Title}
              <h2 class="post-title">
                <a href="{Permalink}">{Title}</a>
              </h2>
            {/block:Title}
            
            <!-- Original Post Content -->
            {block:NotReblog}
              <div class="post-body {block:IfEnablePoetrySpecialFormatting}poetry-formatting{/block:IfEnablePoetrySpecialFormatting}">
                {Body}
              </div>
            {/block:NotReblog}
            
            <!-- Reblog Trail -->
            {block:RebloggedFrom}
              <div class="reblog-trail">
                {block:Reblogs}
                  <div class="reblog-item">
                    <div class="reblog-header">
                      {block:IsActive}
                        <a href="{Permalink}" class="reblog-username">{Username}</a>
                      {/block:IsActive}
                      {block:IsDeactivated}
                        <span class="reblog-username deactivated">{Username}</span>
                      {/block:IsDeactivated}
                    </div>
                    <div class="reblog-content">{Body}</div>
                  </div>
                {/block:Reblogs}
              </div>
            {/block:RebloggedFrom}
          </div>
        {/block:Text}
        
        <!-- All other post types with proper reblog trail support -->
        {block:Answer}
          <div class="post-content answer-post">
            <div class="question-container">
              <div class="asker-info">
                <img src="{AskerPortraitURL-48}" alt="" class="asker-avatar">
                <p class="asker-name">{Asker} asked:</p>
              </div>
              <div class="question">{Question}</div>
            </div>
            
            {block:Answerer}
              <div class="answerer-response">
                <div class="answerer-info">
                  <img src="{AnswererPortraitURL-48}" alt="" class="answerer-avatar">
                  <p class="answerer-name">{Answerer}</p>
                </div>
                <div class="answer">{Answer}</div>
              </div>
            {/block:Answerer}
            
            {block:NotReblog}
              <div class="my-answer">{Replies}</div>
            {/block:NotReblog}
            
            {block:RebloggedFrom}
              <!-- Standard reblog trail here -->
            {/block:RebloggedFrom}
          </div>
        {/block:Answer}
        
        <!-- Continue for all post types: Photo, Quote, Link, Chat, Audio, Video -->
        
        <!-- Post Footer -->
        <footer class="post-footer">
          <div class="post-meta">
            {block:Date}
              <time datetime="{Timestamp}" class="post-date">
                <a href="{Permalink}">{TimeAgo}</a>
              </time>
            {/block:Date}
            
            {block:HasTags}
              <div class="post-tags">
                {block:Tags}
                  <a href="{TagURL}" class="tag">#{Tag}</a>
                {/block:Tags}
              </div>
            {/block:HasTags}
            
            {block:NoteCount}
              <span class="note-count">{NoteCountWithLabel}</span>
            {/block:NoteCount}
          </div>
          
          <div class="post-actions">
            {ReblogButton size="16"}
            {LikeButton size="16"}
          </div>
        </footer>
      </article>
    {/block:Posts}
  </main>
  
  <aside class="sidebar">
    <!-- About Section -->
    <section class="about-widget">
      <h3>About Kenny</h3>
      <div class="about-photo">
        <!-- Use Tumblr's avatar or custom image -->
        <img src="{PortraitURL-128}" alt="Kenny Brown">
      </div>
      <div class="about-text">
        <p>Queer Métis writer and founder of Write Club. BA English (Honours), MRU. 
        Building community for emerging voices in Calgary and beyond.</p>
        
        {block:IfShowCurrentReading}
          <p class="currently-reading">
            <strong>Currently:</strong> {text:Current Reading}
          </p>
        {/block:IfShowCurrentReading}
      </div>
    </section>
    
    <!-- Social Links -->
    <section class="social-widget">
      <h3>Connect</h3>
      <div class="social-links">
        <a href="mailto:{text:Email Address}">Email</a>
        <a href="https://instagram.com/{text:Instagram Handle}">Instagram</a>
        <a href="https://twitter.com/{text:Twitter Handle}">Twitter</a>
        <a href="{RSS}">RSS</a>
      </div>
    </section>
    
    <!-- Substack Embed -->
    {block:IfSubstackEmbedCode}
      <section class="substack-widget">
        <h3>Newsletter</h3>
        {text:Substack Embed Code}
      </section>
    {/block:IfSubstackEmbedCode}
    
    <!-- Blogroll -->
    <section class="blogroll-widget">
      <h3>Fellow Writers</h3>
      <ul class="blogroll">
        {block:IfBlogrollLink1URL}
          <li>
            <a href="{text:Blogroll Link 1 URL}">{text:Blogroll Link 1 Title}</a>
            <span class="blogroll-description">{text:Blogroll Link 1 Description}</span>
          </li>
        {/block:IfBlogrollLink1URL}
        <!-- Repeat for all blogroll entries -->
      </ul>
    </section>
    
    <!-- Write Club Highlight -->
    <section class="write-club-widget">
      <h3>Write Club</h3>
      <p>{text:Write Club Description}</p>
      <a href="/tagged/writeclub" class="write-club-link">See our community →</a>
    </section>
  </aside>
</div>
```

### Pagination
```html
<nav class="pagination">
  {block:Pagination}
    {block:PreviousPage}
      <a href="{PreviousPage}" class="prev-page">← Newer posts</a>
    {/block:PreviousPage}
    
    {block:JumpPagination length="5"}
      {block:CurrentPage}
        <span class="current-page">{PageNumber}</span>
      {/block:CurrentPage}
      {block:JumpPage}
        <a href="{URL}" class="jump-page">{PageNumber}</a>
      {/block:JumpPage}
    {/block:JumpPagination}
    
    {block:NextPage}
      <a href="{NextPage}" class="next-page">Older posts →</a>
    {/block:NextPage}
  {/block:Pagination}
</nav>
```

---

## Mobile Responsiveness

### Breakpoints
- **Desktop**: 1024px+
- **Tablet**: 768-1023px  
- **Mobile**: <768px

### Mobile Adaptations
```css
@media (max-width: 767px) {
  .content-wrapper {
    flex-direction: column;
  }
  
  .sidebar {
    order: -1; /* Move sidebar above posts on mobile */
    width: 100%;
    padding: 1rem;
  }
  
  .hero-section {
    padding: 2rem 1rem;
    min-height: 60vh;
  }
  
  .main-nav {
    flex-wrap: wrap;
    justify-content: center;
  }
}
```

---

## Poetry-Specific Features

### Special Poetry Formatting
```css
.poetry-formatting {
  line-height: 2;
  text-align: center;
  font-family: {font:Poetry Font};
  max-width: 600px;
  margin: 0 auto;
}

.poetry-formatting p {
  margin-bottom: 1.5em;
}

.poetry-formatting br {
  line-height: 2.5; /* Extra space for line breaks in poems */
}
```

### Tag-Based Post Styling
```javascript
// Detect poetry posts by tags and apply special formatting
document.addEventListener('DOMContentLoaded', function() {
  const posts = document.querySelectorAll('.post');
  posts.forEach(post => {
    const tags = post.querySelector('.post-tags');
    if (tags && (tags.textContent.includes('#poetry') || tags.textContent.includes('#poem'))) {
      post.querySelector('.post-body').classList.add('poetry-formatting');
    }
  });
});
```

---

## Cultural Authenticity Guidelines

### Tone & Voice
**What this theme should communicate:**
- "I'm Kenny—writer, community builder, and someone who genuinely cares about your creative journey"
- "This is a space where marginalized voices aren't just welcome, they're centered"
- "Good writing matters, community matters, and your story matters"
- "I'm here to help, not to hustle"

### Design Elements That Support Authenticity
- **Handmade touches**: Slightly imperfect borders, organic shapes
- **Community signals**: Highlight reblogs and interactions, show the conversation
- **Accessibility first**: High contrast, large touch targets, screen reader friendly
- **Cultural respect**: Indigenous design principles of balance and natural elements

### What to Avoid
- Stock photo aesthetics
- Corporate "personal branding" language
- Overly polished, agency-style design
- Aggressive marketing tactics that feel extractive

---

## Accessibility Requirements

### WCAG 2.1 AA Compliance
- **Color Contrast**: Minimum 4.5:1 ratio for normal text, 3:1 for large text
- **Keyboard Navigation**: All interactive elements accessible via keyboard
- **Screen Reader Support**: Proper ARIA labels, semantic HTML structure
- **Focus Indicators**: Clear visual focus states for all interactive elements
- **Alt Text**: Meaningful alt text for all images

### Performance Targets
- **First Contentful Paint**: <2.5 seconds
- **Largest Contentful Paint**: <4 seconds  
- **Cumulative Layout Shift**: <0.1
- **First Input Delay**: <100ms

---

## Implementation Phases

### Phase 1: Core Theme Structure (Week 1)
- Basic HTML template with all Tumblr variables
- CSS framework with responsive grid
- Header, footer, and main content areas
- All post types displaying correctly

### Phase 2: Design & Customization (Week 2)
- Custom color scheme and typography
- Hero section with CTA integration
- Sidebar widgets and custom variables
- Mobile responsive refinements

### Phase 3: Enhancement & Testing (Week 3)
- Poetry-specific formatting features
- Accessibility audit and improvements
- Performance optimization
- Cross-browser testing

---

## Success Metrics

### Community Engagement
- **Increased Ask submissions**: More questions from community members
- **Higher reblog rates**: Content resonating with followers
- **Calendly bookings**: Successful conversion without feeling pushy
- **Comment engagement**: More meaningful interactions on posts

### Technical Performance
- **Core Web Vitals**: All metrics in "good" range
- **Accessibility Score**: 95+ on automated testing
- **Mobile Usage**: Smooth experience across devices
- **Load Performance**: Sub-3-second load times

---

*This theme specification honors Kenny's commitment to authentic community building while providing the professional tools needed to support emerging writers. The goal is to create a digital space that feels like Write Club's in-person workshops—welcoming, supportive, and genuinely focused on helping writers grow.*