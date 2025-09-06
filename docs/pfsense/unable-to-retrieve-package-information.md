# Unable to retrieve package information

### Issue
 When navigating to **System > Package Manager > Available Packages**, you come across the error following message: 

>**Unable to retrieve package information.**

### Resolution

Following this link from Netgate docs: https://docs.netgate.com/pfsense/en/latest/troubleshooting/upgrades.html#upgrade-not-offered-library-errors 

Run these commands in shell:

`pkg-static clean -ay`

`pkg-static install -fy pkg pfSense-repo pfSense-upgrade`