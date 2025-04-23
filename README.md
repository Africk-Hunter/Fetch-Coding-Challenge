## Code Setup

1. Open command prompt and run `git clone https://github.com/fetch-rewards/sre-take-home-exercise-python.git' in desired folder
2. Navigate to folder where files were cloned
3. Run the python script in the command line using 'python main.py .\sample.yaml'

## Problems Identified & Solutions

1. Failure in check_health() function caused by method.upper() failing.
    - I was getting an error when running the code that pointed to the check_health() function that was saying upper() could not be used on NoneType object. Additionally, the instructions made it clear when there is a lack of a method in the YAML file, a 'GET' should be used by default. I went ahead and added a default value to the get() python function where the method would be set to 'GET' if it was NoneType.

2. Time elapsed not being checked
    - The insturctions specified that an endpoint is not valid if it takes longer than 500ms to respond. The code had no checks for this so I went ahead and added one in the line that checks for the status code using `response.elapsed.total_seconds()`.

3. Removing domain port
    - The code already had a line that stripped the '/' and '//' sections from a url but had nothing to remove the port number. Since a link with a port number will have the format `link.com:0000`. I appended to the line to additionally include a split on the colon, effectively removing the port number.

4. Fixed JSON handling in body
    - I noticed the name of the first entry in sample.yaml was called `sample body up`, indicating it should be available. However, when I added a testing print statement I was getting status code `442` from it. I looked up the status code and found it means the server understands the request but cant process it. Immediately I thought the problem was likely the body since that was the main difference compared to the others. I added some code in the check_health() function that checks if the body exists as a string and if it does it converts to a python dictionary. After doing this I started getting a `200` status code and a 50% availabiity percentage for the domain, indicating the error was fixed.