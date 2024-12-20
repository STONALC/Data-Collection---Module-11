# Data-Collection---Module-11
In completing this challenge, I watched the past class videos for support and guidance. Also, I used google co-pilot to help me write and rewrite most of the codes for this challenge. Some of the codes written or rewritten with the guidance of google co-pilot are presented below:

# Create a Beautiful Soup object
from bs4 import BeautifulSoup
import requests

# Define the URL of the page to scrape
url = 'https://static.bc-edx.com/data/web/mars_news/index.html'

# Use requests to get the content of the page
response = requests.get(url)
html_content = response.text

# Create a Beautiful Soup object
soup = BeautifulSoup(html_content, 'lxml')

# Print the title of the page to verify
print(soup.title.text)

from bs4 import BeautifulSoup
import requests

# Define URL of the page to scrape
url = 'https://static.bc-edx.com/data/web/mars_news/index.html'

# Make a request to get the content of the page
response = requests.get(url)
web_content = response.content

# Parse the HTML content using BeautifulSoup
soup = BeautifulSoup(web_content, 'html.parser')

# Find the text elements you are interested in
text_elements = soup.find_all('p')

# Loop through the text elements
for element in text_elements:
    print(element.get_text())
    
# Extract the title and preview text from the elements
news_items = soup.find_all('div', class_='list_text')

# Store each title and preview pair in a dictionary
news_title = []

# Define a dictionary
dict = {"title": "NASA's MAVEN Observes Martian Light Show Caused by Major Solar Storm", 
        "Preview": "For the first time in its eight years orbiting Mars, NASA's MAVEN mission witnessed two different types of ultraviolet aurorae simultaneously, the result of solar storms that began on Aug. 27."}

# Initialize the list
my_list = []

# Add the dictionary to the list
my_list.append(dict) 

import json
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

def scrape_mars_news():
    # Path to your ChromeDriver executable
    driver_path = 'C:/Users/stona/OneDrive/Documents/bin/chromedriver.exe'

    # Set up Chrome options
    options = webdriver.ChromeOptions()

    # Set up the Chrome service
    service = ChromeService(executable_path=driver_path)

    # Initialize the browser with the service and options
    browser = webdriver.Chrome(service=service, options=options)

    try:
        # Visit the Mars news site
        browser.get('https://static.bc-edx.com/data/web/mars_news/index.html')

        # Allow some time for the page to load
        WebDriverWait(browser, 10).until(EC.presence_of_element_located((By.CLASS_NAME, 'list_text')))

        # Scrape titles and preview texts from Mars
        articles = browser.find_elements(By.CLASS_NAME, 'list_text')

        # List to hold titles and previews
        news_list = []

        # Loop through each article and extract the title and preview text
        for article in articles:
            title_element = article.find_element(By.TAG_NAME, 'a')
            preview_element = article.find_element(By.CLASS_NAME, 'article_teaser_body')
            
            title = title_element.text
            preview = preview_element.text
            
            news_list.append({'title': title, 'preview': preview})

        # Print the titles and preview texts
        for news in news_list:
            print(f"Title: {news['title']}")
            print(f"Preview: {news['preview']}\n")

        # Export the data to a JSON file
        with open('mars_news.json', 'w') as json_file:
            json.dump(news_list, json_file, indent=4)
        print("Data exported to mars_news.json successfully!")

    finally:
        # Quit the browser
        browser.quit()

# Execute the scrape_mars_news function
scrape_mars_news()


# Import dependencies
from splinter import Browser
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options

# Set the path to your chromedriver
executable_path = r'C:\Users\stona\OneDrive\Documents\bin\chromedriver.exe'

# Ensure to provide the correct path to the executable
service = Service(executable_path=executable_path)
options = Options()

# Create a browser instance
browser = Browser('chrome', service=service, options=options)

# Visit the website
url = 'https://static.bc-edx.com/data/web/mars_facts/temperature.html'
browser.visit(url)

# Print the title of the page to verify
print(browser.title)

# Close the browser
browser.quit()

from selenium import webdriver
from selenium.webdriver.chrome.service import Service

# Specify the path to the ChromeDriver executable
chromedriver_path = r'C:\Users\stona\OneDrive\Documents\bin'

# Install ChromeDriver
service = Service(executable_path=chromedriver_path)

# Initialize the browser
browser = webdriver.Chrome(service=service)

# Visit the website
url = 'https://static.bc-edx.com/data/web/mars_facts/temperature.html'
browser.get(url)

# Interact with the page as needed
# For example, find an element and print its text
title_element = browser.find_element('tag name', 'h1')
if title_element:
    print(title_element.text)

# Close the browser
browser.quit()