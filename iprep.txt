#!/usr/bin/python3

import requests
import csv
import apivoid

# Set up apivoid API endpoint and API key
# API_ENDPOINT = 'https://endpoint.apivoid.com/iprep/v1/pay-as-you-go/'
API_KEY = 'YOUR_API_KEY_HERE'

# Open the file containing the IP addresses
with open('sourcefile.txt', 'r') as f:
    ip_addresses = f.readlines()

# Open the CSV file for writing
with open('iprep.csv', 'w', newline='') as csv_file:
    writer = csv.writer(csv_file)

    # Write the header row
    writer.writerow(['IP Address', 
                     'Hostname', 
                     'Detections Count', 
                     'Detected By',
                     'Country',
                     'Continent',
                     'Region',
                     'City',
                     'Latitude',
                     'Longitude',
                     'ISP',
                     'Is Proxy',
                     'Is Web Proxy',
                     'Is VPN',
                     'Is Hosting',
                     'Is Hosting',
                     'Is Tore'])

    # Iterate through the list of IP addresses and check their reputation using apivoid
    for ip_address in ip_addresses:
        ip_address = ip_address.strip()  # Remove any whitespace or newline characters
        # print(ip_address)
        data = apivoid.make_query("iprep", {"key":"dd958d7e0542a92a3c38a1c3e6354db3dcbc7879","ip":ip_address})
        # data = requests.get(url='https://endpoint.apivoid.com/iprep/v1/pay-as-you-go/?key='+API_KEY+'&ip='+ip_address)

        if(data):
            if(data.get('error')):
                print("Error: "+data['error'])
            else:
                print("IP: "+data['data']['report']['ip'])
                print("Hostname: "+str(data['data']['report']['blacklists']['detections']))
                print("---")
                print("Detections Count: "+str(data['data']['report']['blacklists']['detections']))
                print("Detected By: "+apivoid.get_detection_engines(data['data']['report']['blacklists']['engines']))
                print("---")
                print("Country: "+data['data']['report']['information']['country_code']+" ("+data['data']['report']['information']['country_name']+")")
                print("Continent: "+data['data']['report']['information']['continent_code']+" ("+data['data']['report']['information']['continent_name']+")")
                print("Region: "+data['data']['report']['information']['region_name'])
                print("City: "+str(data['data']['report']['information']['latitude']))
                print("Latitude: "+str(data['data']['report']['information']['latitude']))
                print("Longitude: "+str(data['data']['report']['information']['longitude']))
                print("ISP: "+data['data']['report']['information']['isp'])
                print("---")
                print("Is Proxy: "+str(data['data']['report']['anonymity']['is_proxy']))
                print("Is Web Proxy: "+str(data['data']['report']['anonymity']['is_webproxy']))
                print("Is VPN: "+str(data['data']['report']['anonymity']['is_vpn']))
                print("Is Hosting: "+str(data['data']['report']['anonymity']['is_hosting']))
                print("Is Tor: "+str(data['data']['report']['anonymity']['is_tor']))
                ip=data['data']['report']['ip']
                hostname=str(data['data']['report']['blacklists']['detections'])
                detectionscount=str(data['data']['report']['blacklists']['detections'])
                detectedby=apivoid.get_detection_engines(data['data']['report']['blacklists']['engines'])
                country=data['data']['report']['information']['country_code']+" ("+data['data']['report']['information']['country_name']+")"
                continent=data['data']['report']['information']['continent_code']+" ("+data['data']['report']['information']['continent_name']+")"
                region=data['data']['report']['information']['region_name']
                city=str(data['data']['report']['information']['latitude'])
                latitude=str(data['data']['report']['information']['latitude'])
                longitude=str(data['data']['report']['information']['longitude'])
                isp=data['data']['report']['information']['isp']
                isproxy=str(data['data']['report']['anonymity']['is_proxy'])
                iswebproxy=str(data['data']['report']['anonymity']['is_webproxy'])
                isvpn=str(data['data']['report']['anonymity']['is_vpn'])
                ishosting=str(data['data']['report']['anonymity']['is_hosting'])
                istor=str(data['data']['report']['anonymity']['is_tor'])
        else:
                print("Error: Request failed")

        # Write the data to the CSV file
        writer.writerow([ip, hostname, detectionscount, detectedby, country, continent, region, city, latitude, longitude, isp, isproxy, iswebproxy, isvpn, ishosting, istor])

print('Done!')

