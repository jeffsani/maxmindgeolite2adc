# maxmindgeolite2adc

Initial version: 1.0
Date: 3/29/2022
Author: Jeff Sani

Description:
This script will automate the refresh of the Citrix ADC (NetScaler) InBuilt MaxMind GeoLite2 Location Database files Citrix_Netscaler_InBuilt_GeoIP_DB_IPv4 and Citrix_Netscaler_InBuilt_GeoIP_DB_IPv6 which are used with Static Proximity GSLB and Policy Expressions that reference a Location.  The main benefit of this script is to refresh these location files with up-to-date versions as these are not updated via on-box automation or new firmware installs.  The script will run weekly, download the maxmind free Geolite2 City or Country DB (CSV Format) if it has been refreshed, perform a checksum on the file to verify file integrity, convert it to the required NetScaler location db format, and upload the new files to the requisite directory where the InBuilt files are located. 

According to the maxmind web site, the GeoIP Databases are updated each Tuesday - see https://support.maxmind.com/hc/en-us/articles/4408216129947-Download-and-Update-Databases.  The init script configures a cron job which is scheduled to run every Wednesday morning at 1:00AM.  

Requirements:
To implement this script you will need the following:

1. a Geolite2 Account setup at https://www.maxmind.com/en/geolite2/signup?lang=en
2. a License Key - created post account setup and generated at https://www.maxmind.com/en/accounts/696069/license-key
3. Permalinks to the Country and/or City Geo IP Databases in CSV format 
4. A host or container to run this on
5. This conversion tool https://github.com/citrix/MaxMind-GeoIP-Database-Conversion-Citrix-ADC-Format
6. unzip utility
7. Environment variables set for the user running the script that contain the Citrix ADC user/pass, the Citrix ADC

Required Packages (for Linux Host):
- unzip libwww-perl libmime-lite-perl libnet-ip-perl git

Automated Setup (For Linux Host):
- Complete steps 1-3 in the requirements
- Clone the repo into the desired directory on your linux host
    git clone https://github.com/jeffsani/maxmindgeolite2adc.git git <directory> (directory is optional)
- Run the init.sh script
