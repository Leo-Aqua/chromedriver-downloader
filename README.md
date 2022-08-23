# chromedriver-downloader
Automatically downloads the correct version of chromedriver.exe

## Just add following code:

```Python
import requests
import os
from zipfile import ZipFile
from win32com.client import Dispatch
if os.path.exists('chromedriver.exe'): # Check if chromedriver.exe exists
    print('Chromedriver executable exists, skipping')
else:
    print('Downloading chromedriver executable...')
    def get_version_via_com(filename): # Get Chrome version using Dispatch
        parser = Dispatch("Scripting.FileSystemObject")
        try:
            crm_version = parser.GetFileVersion(filename)
        except Exception:
            return None
        return crm_version
    if __name__ == "__main__":
        paths = [r"C:\Program Files\Google\Chrome\Application\chrome.exe",
                r"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"]
        crm_version = list(filter(None, [get_version_via_com(p) for p in paths]))[0]
    global ncrm_version
    ver = crm_version.startswith('103')
    if ver == True:
        ncrm_version = '103.0.5060.134'
    ver = crm_version.startswith('104')
    if ver == True:
        ncrm_version = '104.0.5112.79'
    ver = crm_version.startswith('105')
    if ver == True:
        ncrm_version = '105.0.5195.19'
    url = f'https://chromedriver.storage.googleapis.com/{ncrm_version}/chromedriver_win32.zip' # Download Chromedriver
    response = requests.get(url)
    open("driver.zip", "wb").write(response.content)
    zf = ZipFile('driver.zip', 'r')
    zf.extractall('.')
    zf.close()
    os.remove('driver.zip')
    print('Done!')
    
#Your code goes here!
```

## Currently supported versions:
>103.0.5060.134
>
>104.0.5112.79
>
>105.0.5195.19


# Features:
1. Automatically get correct chromedriver version
2. Yust add it to the top of your code
3. After downloading chromedriver once, It won't affect speed of your script at all!

###### Made with code by Leo Aqua
