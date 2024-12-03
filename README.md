# GeneratingQuotes
import requests
from bs4 import BeautifulSoup
URL = "http://quotes.toscrape.com"
response = requests.get(URL)
if response.status_code == 200:
    soup = BeautifulSoup(response.text, 'html.parser')
    quotes = soup.find_all('span', class_='text')  
    authors = soup.find_all('small', class_='author')  
    tags = soup.find_all('div', class_='tags')
    for i in range(len(quotes)):
        print(f"Quote: {quotes[i].text}")
        print(f"Author: {authors[i].text}")
        tag_list = [tag.text for tag in tags[i].find_all('a', class_='tag')]
        print(f"Tags: {', '.join(tag_list)}")
        print('-' * 50)
else:
    print("Failed to retrieve the webpage. Status code:", response.status_code)
