# Mission-to-Mars

## Overview
### Purpose
> Robin's web app is looking good and functioning well, but she wants to add more polish to it. She had been admiring images of Mars’s hemispheres online and realized that the site is scraping-friendly. She would like to adjust the current web app to include all four of the hemisphere images. To do this, you’ll use BeautifulSoup and Splinter to scrape full-resolution images of Mars’s hemispheres and the titles of those images, store the scraped data on a Mongo database, use a web application to display the data, and alter the design of the web app to accommodate these images.

### Resources

- Languages: Python 3.7.10, Javascript, HTML, CSS (Bootstrap)
- Interface: Jupyter Notebook, Visual Studio Code
- Environment: Miniconda
- Packages and Software: Beautiful Soup, Splinter, ChromeDriverManager, Pandas, PyMongo, Flask, MongoDB
- Data Source: [Astropedia](https://astrogeology.usgs.gov/search/results?q=hemisphere+enhanced&k1=target&v1=Mars)

## Results
### 1) Scrape High-Resolution Mars Hemisphere Images and Titles
Look for the scrape of the image URLs and titles into a dictionary that can then be added to the web app.
```
for i in range(4):
    
    # Create empty dictionary to hold items
    hemisphere = {}
    
    # Click on link of item to navigate to the page
    browser.find_by_text(hemi_items[i].text).click()
    
    # Find HTML object and create HTML parser
    new_page = browser.html
    new_soup = soup(new_page, 'html.parser')
    
    # Find picture source using Sample image anchor tag
    hemisphere["img_url"] = url + str(new_soup.find('a', string='Sample')['href'])
    
    #Find title
    hemisphere["title"] = new_soup.find('h2', class_='title').text
    
    # Append data to list
    hemisphere_image_urls.append(hemisphere)
    
    # Browser go back
    browser.back()
```
### 2) Update the Web App with Mars Hemisphere Images and Titles
The gist of the for loop below (disregarding div tags for a clearer look at the elements added).
```
{% for hemisphere in mars.hemispheres %}
  -
  -
  <img src="{{hemisphere.img_url | default('static/images/error.png', true) }}"
      class = "img-thumbnail"
      alt = "..."/>
  -
  <h3>{{hemisphere.title}}</h3>
  -
  -
  -
  {% endfor %}
      
```
### 3) Add Bootstrap 3 Components
Example of added CSS elements.
```
<a class="btn btn-default btn-lg" style="background-color: #d29a90" href="/scrape" role="button">
```
