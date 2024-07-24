Redirecting visitors to country-specific pages can enhance user experience by presenting content in the appropriate language and tailored to local preferences. This can be achieved using JavaScript to detect the visitor's country and redirect them accordingly. In this article, we'll demonstrate how to accomplish this using a simple script.

Step-by-Step Guide
1. Setting Up the Endpoint
First, we need an endpoint that returns the visitor's country code based on their IP address. For this example, we'll use https://apip.cc/json.

2. Writing the JavaScript
Below is the JavaScript code that performs the redirection based on the visitor's country code. If the country code doesn't match the specified countries, the script defaults to google.com.


<script>
var endpoint = 'https://apip.cc/json';
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        var response = JSON.parse(this.responseText);
        if(response.status !== 'success') {
            console.log('Query failed: ' + response.message);
            return;
        }
        // Redirect based on the country code
        switch(response.CountryCode) {
            case "GB":
                window.location.replace("https://google.co.uk/");
                break;
            case "CA":
                window.location.replace("https://google.ca/");
                break;
            case "SG":
                window.location.replace("https://google.com.sg/");
                break;
            default:
                window.location.replace("https://google.com/");
        }
    }
};
xhr.open('GET', endpoint, true);
xhr.send();
</script>


Explanation of the Script
Endpoint Declaration: The endpoint variable holds the URL to the service that returns the visitor's country information.

XMLHttpRequest Setup: An XMLHttpRequest object (xhr) is created to send a request to the endpoint.

Handling the Response:

The onreadystatechange function is triggered every time the state of the xhr object changes.
When the request is complete (readyState == 4) and successful (status == 200), the response is parsed as JSON.
If the response status is not 'success', an error message is logged.
Country Code Redirection:

A switch statement checks the CountryCode in the response.
If the CountryCode is "GB", "CA", or "SG", the script redirects the visitor to the corresponding Google domain.
If the CountryCode does not match any specified case, the script defaults to google.com.
Testing the Script
To test the script:

Place the script in the <head> or <body> section of your HTML file.
Ensure the endpoint https://apip.cc/json is accessible and returns the correct data.
Open the HTML file in a browser. Depending on your IP address, you should be redirected to the appropriate Google domain or the default domain (google.com).

Conclusion
By following this guide, you can implement a country-based redirection mechanism on your website using JavaScript. This approach ensures that visitors are directed to the most relevant version of your site, improving user experience and engagement.

Source: <a href="https://apip.cc/redirect-visitors-by-country-using-javascript.html">How to Redirect Visitors by Country Using JavaScript</a>
