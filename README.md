import requests
import json

def get_linkedin_profiles(company_name):
    api_key = "29ae101c9fefe83c485cc04c73037a9411853689fa937089188bdee46fb5eaf4"  # Replace with your SerpAPI key
    search_query = f"{company_name} site:linkedin.com"
    
    params = {
        "engine": "google",
        "q": search_query,
        "api_key": api_key
    }
    
    response = requests.get("https://serpapi.com/search", params=params)
    
    if response.status_code != 200:
        print("Failed to fetch data")
        return None
    
    results = response.json().get("organic_results", [])
    linkedin_links = [result["link"] for result in results if "linkedin.com" in result["link"]]
    
    return linkedin_links

if __name__ == "__main__":
    company_name = input("Enter the company name: ")
    linkedin_profiles = get_linkedin_profiles(company_name)
    
    if linkedin_profiles:
        print("LinkedIn Profiles:")
        for link in linkedin_profiles:
            print(link)
    else:
        print("No LinkedIn profiles found.")

