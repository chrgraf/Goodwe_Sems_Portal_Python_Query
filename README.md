# Goodwe_Sems_Portal_Python_Query
sample python-code to Query the Goodwe Sems-Portal via HTTPS


Dear all,

this small script provides basic building-blocks to query the GoodWe Sems-Portal.
The token can be-reused, means subsequent calls can make use of an existing authentication-token.
If the tokes expires, the script will renew the token and continue querying the portal.

## credentials
You need to create a credentials file called: sems_config.py

While Username and password (single or doublequotes are just fine) are trivial, the power-station-id is somewhat non-trivial.
Easiest way to aquire it, is to login to via your PC,Tablet,.. to the Sems-Portal and look at the "resulting"URL after you looged-in successfully.
it will read: https://www.semsportal.com/PowerStation/PowerStatusSnMin/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  

Check the xxx stuff - that your ID!

```
behn@rpi5:~/jk_venv $ cat sems_config.py
username = "<your email-Address>"
pw = "your password on the Goodwe Sems Portal"
power_station_id = "<aquire this from the URL as described aobve>"
```

# How to call:

behn@rpi5:~/jk_venv $ ./sems.py

## Output
```
######################################
# query_generator
######################################
url used: https://eu.semsportal.com/api/v2/PowerStation/GetMonitorDetailByPowerstationId
https://eu.semsportal.com/api/v2/PowerStation/GetMonitorDetailByPowerstationId
{'Content-Type': 'application/json', 'Token': '{"version":"v2.1.0","client":"ios","language":"en","timestamp":"","uid":"","token":""}', 'Content-Length': '58'}
response status code:  200
Query-String used for generator Query:  {"version":"v2.1.0","client":"ios","language":"en","timestamp":"","uid":"","token":""}
code: 100001
>>>Query generator failed
>>>Lets aquire a new token and retry

######################################
# Function: get_token
######################################
url used: https://www.semsportal.com/api/v2/Common/CrossLogin
derived authentication credentials
----------------------------------
  Token    :  <>
  UID      :  <>
  timestamp:  1710860766663
  api      :  https://eu.semsportal.com/api/

######################################
# query_generator
######################################
url used: https://eu.semsportal.com/api/v2/PowerStation/GetMonitorDetailByPowerstationId
https://eu.semsportal.com/api/v2/PowerStation/GetMonitorDetailByPowerstationId
...
response status code:  200
...
>>>Query generator was successful

######################################
# get_battery_power
######################################
Parsing the JSON-String to derive Battery :  49.9V/0.8A/40W
 - battery-Power[W], Battery_Power[A] 0.8 40
Reversing the logic and multiplying the values with -1
 - battery-Power[W], Battery_Power[A] -0.8 -40
Success
```

# License
MIT License

Copyright (c) [2024] [Christian Graf]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
