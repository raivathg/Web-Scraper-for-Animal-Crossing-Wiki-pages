# Web-Scraper-for-Animal-Crossing-Wiki-pages
This github repo has a web scraper which first takes in the page where all the links of Animal Crossing is listed. It then crawls through each of the pages listed and get the overall pages present in the Animal Crossing Wiki links.

# Pre-requisites
To install the required packages for running the Python script, you can follow the steps below:

1. Install Python: If you don't have Python installed on your system, you can download and install the latest version from the official Python website (https://www.python.org/downloads/). Follow the installation instructions for your operating system.

2. Install pip: Pip is a package manager for Python that allows you to easily install and manage Python packages. If you're using Python version 2.7.9 or later (including Python 3.x), pip is already included with Python. If not, you can download and install it by following the instructions here: https://pip.pypa.io/en/stable/installation/

3. Install the required packages: Once you have pip installed, open a command prompt (on Windows) or terminal (on Mac or Linux) and run the following commands:

```
pip install requests
pip install beautifulsoup4
pip install crontab
```

4. The hashlib and json modules are included in Python by default, so no installation is needed for these.

# Explanation of what each of the function performs
Here is a brief description of each function:

1. find_next_url(soup): This function takes a BeautifulSoup object as input and searches for the URL of the next page by finding the link with "Next page" in its description.

2. fetch_all_sub_main_pages_of_animal_crossing(base_url, start_url): This function fetches all the main pages for the "Animal Crossing" wiki by following the "Next page" links on the wiki until there are no more pages to fetch. It returns a list of URLs for each main page.

3. get_all_links_in_page(url, base_url): This function takes a URL as input and returns a list of URLs for each subpage on the wiki. It scrapes the HTML content of the input URL and finds all the subpage links in the "mw-allpages-body" div.

4. scrape_single_url_for_data(url): This function scrapes a single URL for data on the "Animal Crossing" wiki. It extracts the title, summary, and content of the wiki page and returns a dictionary with this data.

5. create_or_check_for_changes_in_wiki_pages(all_urls): This function creates or updates a JSON file that stores the SHA256 hash for each page on the wiki. It compares the current SHA256 hash to the hash stored in the JSON file to see if any changes have been made to the page. If there are changes, it prints a message indicating which fields have been modified.

# How to schedule the scraper to run weekly
Navigate to the main directory of Web-Scraper-for-Animal-Crossing-Wiki-pages. Open scraper_cron.py file and change the user and file path of the animal_crossing_web_scraper.py file as present in your computer. Then run the following command from inside the main directory

```
python scraper_cron.py
```

To verify if the web scraper is scheduled to run weekly execute the following command. 
```
crontab -l
```

The output of the above command should look something like below, but the file path for your python file will be different.
```
0 0 * * 1 python /Users/rgirish/Documents/My_Projects/Splore_assignment/animal_crossing_web_scraper.py
```

# Time taken
When animal_crossing_web_scraper.py is first executed and it has create new documents for each of the pages it takes 22 mins to scrape through 6981 pages and create documents for each.

Once the documents have been created for each of the pages and animal_crossing_web_scraper.py is executed again, it still takes 22 mins to scrape through all 6981 pages and compare if there has been any changes. If there are any changes it will print the output to a output.log file, with the URL where the change has happened and it also shows the previous and current versions of that URL.
