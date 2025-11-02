# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based academic personal website for displaying publications, research highlights, and CV information. The site is designed to be deployed on GitHub Pages and uses the Minima theme with custom styling.

## Development Commands

### Local Development Setup

The project uses Conda for Ruby environment management:

```bash
# Create and activate conda environment (first time only)
conda create -n jekyll-env
conda activate jekyll-env
conda install -c conda-forge gcc gxx make openssl pkg-config ruby

# Install Ruby dependencies
bundle install
```

### Running the Site Locally

```bash
# Start Jekyll development server
bundle exec jekyll serve

# Site will be available at http://localhost:4000
```

**Important**: Changes to `_config.yml` require restarting the Jekyll server to take effect.

## Site Architecture

### Configuration and Data Structure

The site uses a data-driven architecture where content is separated from presentation:

- **`_config.yml`**: Main site configuration containing personal information (name, email, position, social links, Google Analytics ID, etc.)
- **`_data/` directory**: Contains YAML files that drive the site content:
  - `publications.yml`: Research publications with metadata (title, venue, authors, project pages, arxiv links, images/videos)
  - `authors.yml`: Author database mapping author IDs to names and websites. Uses `is_me: true` to mark the site owner
  - `highlights.yml`: Featured research highlights displayed as cards on homepage
  - `education.yml`: Educational background for CV page
  - `employment.yml`: Work experience for CV page
  - `news.yml`: News/updates (if used)

### Page Templates

The site uses two main HTML templates (not in `_layouts/` - they are standalone HTML files with Jekyll front matter):

- **`index.html`**: Homepage with hero section, highlights cards, and publications list
- **`cv.html`**: CV page with education, employment, and publications

Both pages use:
- Bulma CSS framework for styling
- Font Awesome and Academicons for icons
- jQuery for interactivity
- Google Analytics tracking

### Publications Display System

Publications support:
- Static images (`image` field) with optional hover-activated video overlays (`image_mouseover` field for MP4 files)
- Author linking via the `authors.yml` database
- Multiple external links (project page, arxiv, PDF, GitHub)
- Awards/special designations (e.g., "Oral Presentation", "Journal Cover")

### Static Assets

- **`css/`**: Bulma CSS framework, Font Awesome, and custom styles (`index.css`, `cv.css`)
- **`js/`**: Font Awesome JS and custom scripts (`index.js`)
- **`images/`**: Publication images/videos and portrait photo
- **`_sass/`**: SCSS partials for custom styling

## Content Updates

### Adding a New Publication

1. Add entry to `_data/publications.yml`:
```yaml
- id: unique-id
  title: "Paper Title"
  venue: "Conference/Journal, Year"
  description: "Brief description"
  project_page: https://project-url.github.io
  arxiv: 1234.56789
  github: username/repo  # optional
  image: thumbnail.jpg
  image_mouseover: video.mp4  # optional
  authors:
    - author_id1
    - author_id2
  awards:  # optional
    - "Oral Presentation"
```

2. If new authors are referenced, add them to `_data/authors.yml`:
```yaml
author_id:
  first_name: First
  middle_name: Middle  # optional
  last_name: Last
  website: https://author-website.com
  is_me: false  # set to true only for the site owner
```

3. Add image/video assets to `images/` directory

### Updating Personal Information

Edit `_config.yml` to update name, position, email, social media handles, and site description. Remember to restart the Jekyll server after changes.

## Deployment

The site is configured for GitHub Pages deployment at `kdyun0118.github.io`. Push changes to the master branch to trigger automatic deployment.