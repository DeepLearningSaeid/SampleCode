# SampleCode

import geoip2.database

def ip_to_zip(ip_address, db_path='GeoLite2-City.mmdb'):
    try:
        reader = geoip2.database.Reader(db_path)
        response = reader.city(ip_address)
        zip_code = response.postal.code
        reader.close()
        return zip_code
    except Exception as e:
        print(f"Error: {e}")
        return None

ip_address = '8.8.8.8'  # Replace this with the IP address you want to convert
zip_code = ip_to_zip(ip_address)

if zip_code:
    print(f"Zip code for IP address {ip_address}: {zip_code}")
else:
    print("Unable to find a zip code for the given IP address.")
    
    
    
    import requests

def ip_to_zip(ip_address, api_key):
    try:
        # Use Azure Maps IP to Location API to get latitude and longitude
        ip_location_url = f"https://atlas.microsoft.com/ip/location/json?subscription-key={api_key}&api-version=1.0&ip={ip_address}"
        ip_location_response = requests.get(ip_location_url).json()
        lat, lon = ip_location_response['location']['coordinates']

        # Use Azure Maps Reverse Geocoding API to get zip code
        reverse_geocode_url = f"https://atlas.microsoft.com/search/address/reverse/json?subscription-key={api_key}&api-version=1.0&query={lat},{lon}&location=US"
        reverse_geocode_response = requests.get(reverse_geocode_url).json()

        # Extract zip code from the API response
        zip_code = None
        for address in reverse_geocode_response['addresses']:
            if 'postalCode' in address:
                zip_code = address['postalCode']
                break

        return zip_code

    except Exception as e:
        print(f"Error: {e}")
        return None

ip_address = '8.8.8.8'  # Replace this with the IP address you want to convert
api_key = 'YOUR_AZURE_MAPS_API_KEY'  # Replace this with your Azure Maps API key

zip_code = ip_to_zip(ip_address, api_key)

if zip_code:
    print(f"Zip code for IP address {ip_address}: {zip_code}")
else:
    print("Unable to find a zip code for the given IP address.")

Sign up for an Azure Maps account and obtain an API key. You can follow the instructions here: https://docs.microsoft.com/en-us/azure/azure-maps/how-to-manage-authentication
