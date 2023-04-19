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
