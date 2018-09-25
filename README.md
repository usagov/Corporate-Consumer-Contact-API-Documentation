# NOTE: This API has been deprecated and is no longer active.  For a list of active GSA APIs, please visit [https://open.gsa.gov/api/](https://open.gsa.gov/api/).  

------------------

## Corporate Consumer Contact API Documentation

## On This Page
*   [About the API](#about-the-api)
*   [About the Data](#about-the-data)
*   [Accessing the API](#accessing-the-api)
*   [API Methods](#api-methods)
*   [Terms of Service](#terms-of-service)

## About the API

We make the Corporate Consumer Contact listing found in the [Consumer Action Handbook (PDF)](http://publications.usa.gov/USAFileDnld.php?PubType=P&PubID=5131&httpGetPubID=0) available via a REST API. The API programmatically returns all of the information contained in the directory, or you can query the API to return just a subset of the available information.

If you are using the Corporate Consumer Contact API and have questions, feedback, or want to tell us about your product, please [e-mail us](mailto:usagov-developers@gsa.gov).

## About the Data

The data in the Corporate Consumer Contact API is based on the content you can find in the Corporate Consumer Contact listing in the [Consumer Action Handbook (PDF)](http://publications.usa.gov/USAFileDnld.php?PubType=P&PubID=5131&httpGetPubID=0). We gather this data manually, as it can sometimes be difficult for consumers to find out how they can contact a corporation. As this is a consumer focused dataset, corporations included in the API are corporations that directly interact with consumers.

There is no schedule for data updates; we update the data continually, and as needed. However, all data is reviewed at least annually.

If you have suggestions about what types of data you would like to see in the Corporate Consumer Contact API, please [e-mail us](mailto:usagov-developers@gsa.gov).

## Accessing the API

Our Corporate Consumer Contact API is accessible via HTTP GET requests and does not require a login or API key to use.

The base URL for the API is https://www.usa.gov/api/USAGovAPI/corporate/contacts.{format}/. Append the API call you’d like to make to this URL.

Currently, three output formats are available:

1.  JSON (such as https://www.usa.gov/api/USAGovAPI/corporate/contacts.json/contacts)
2.  XML (such as https://www.usa.gov/api/USAGovAPI/corporate/contacts.xml/contacts)
3.  JSONP (such as https://www.usa.gov/api/USAGovAPI/corporate/contacts.jsonp/contacts?callback=callmemaybe). When requesting JSONP, you should include a callback parameter with the name of the callback function you would like called.

For the purposes of this documentation, only JSON sample calls and results will be shown.

### Interactive Documentation for the API

The interactive documentation for the Corporate Consumer Contact API has been discontinued as we're preparing to deprecate this API in its current form.  The content will still be available, but the format of the API will be slightly different as we launch an improved API that provides access not just to directory content, but to all of the content available on USA.gov and GobiernoUSA.gov.

### API Data Model

The following fields are associated with directory records. Please note that not every record has data in every field, and the API will only return completed fields.

*   **Id** - A unique identifier for each directory record
*   **Name** – The name of the corporation.
*   **Description** – Any notes about contacting the corporation.
*   **Subdivision** – Used for mailing letters to the corporation..
*   **Street1** – A first line of address information (such as the street address) for contacting the corporation.
*   **Street2** – A second line of address information for contacting the corporation.
*   **City** – The city of the corporation's mailing address.
*   **StateTer** – The state of the corporation's mailing address.
*   **Zip** – The postal zip code of the corporation's mailing address.
*   **Email** – The e-mail address for contacting the corporation.
*   **Phone** – The phone number to be used when contacting the corporation (may contain more than one).
*   **TTY** – The TTY number to be used when contacting the corporation (may contain more than one).
*   **Tollfree** – The toll-free number to be used when contacting the corporation (may contain more than one).
*   **URI** – The URL to access the corporation’s complete directory record via the API.

**URLs**

The API returns URLs that can be used to contact the corporation in a Web_URL array.

For each of these URLs, the following sub-data elements are returned:

*   **Url** – The URL to the web page.
*   **Description** – A description of the URL.
*   **Language** – Whether the web page located at the URL is in English (en) or Spanish (es).

## API Methods

### Contacts

Contacts is a general purpose call that, by default, will return all of the corporate directory records. However, you can pass parameters into the contacts call that allow you to filter the records returned by the API in powerful ways.

**Parameters**

**query_filter** – Return only corporate directory records that meet the criteria you enter into this parameter. In general, the filter takes the form of {field_name}::{value}[|{field_name}::{value}]*. Additionally, for names, you can perform substring searches by surrounding {value} with asterisks.

For example, if you want to return all corporations that have the word “app” in their title, you can use a query_filter of name::*app*. Likewise, if you want to find all corporations who have either "car" in their name or have their main address in Virginia, you can use a query_filter of: name::*car*|state::VA

See the data model above for a list of field names that you can query on.

**result_filter** – Return only the fields listed here (separated by |) as opposed to every field in each directory record. For example, use a result_filter of name|phone to return only names and phone numbers.

See the data model above for a list of field names that you can specify be returned.

**sort** – Allows you to specify the sort order of the returned agency directory records. For example, use a sort of name to sort the results by the agency’s name. You can also cause the sort to go in descending order by adding a - before the field name, such as -name.

See the data model above for a list of field names that you can sort the results on.

**X-Range HTTP Request Header** – You can limit the results returned by the API by including an X-Range HTTP header in your GET request, with a value of items=x to y, where x is the lower limit and y is the upper limit of the results to be returned.

The API will return a X-Content-Range header in its HTTP response that indicates which results are being returned, and the total number of results for your query. For example: X-Content-Range: 11-20/21.

### Sample Results

The Contacts endpoint will return an array of objects, such as:

    {
      "Contact": [
        {
          "Id": "45900",
          "URI": "http://www.usa.gov/api/USAGovAPI/corporate/contacts.json/contact/45900",
          "Language": "en",
          "Name": "Carvel Corporation",
          "Source_Url": "http://www.usa.gov/notpublishable.shtml",
          "Street1": "11401 Century Oaks Terrace, Suite",
          "City": "Austin",
          "StateTer": "TX",
          "Zip": "78758",
          "Tollfree": [
            "1-800-322-4848"
          ],
          "Web_Url": [
            {
              "Url": "http://www.carvel.com",
              "Description": "Carvel Corporation",
              "Language": "en"
            }
          ],
          "Description": "written inquiries only",
          "Subdivision": "Retail Stores/Food Service"
        },
        {
          "Id": "45904",
          "URI": "http://www.usa.gov/api/USAGovAPI/corporate/contacts.json/contact/45904",
          "Language": "en",
          "Name": "Casual Male Retail Group",
          "Source_Url": "http://www.usa.gov/notpublishable.shtml",
          "Street1": "555 Turnpike St.",
          "City": "Canton",
          "StateTer": "MA",
          "Zip": "02021",
          "Tollfree": [
            "1-800-746-7395"
          ],
          "Email": "info@casualmale.com",
          "Web_Url": [
            {
              "Url": "http://twitter.com/casualmalexl",
              "Description": "Casual Male Retail Group Casual Males Twitter Page",
              "Language": "en"
            },
            {
              "Url": "http://www.facebook.com/OfficialCasualMaleXL",
              "Description": "Casual Males Facebook Page",
              "Language": "en"
            },
            {
              "Url": "http://www.cmrginc.com",
              "Description": "",
              "Language": "en"
            }
          ],
          "Subdivision": "Customer Service"
        }
      ]
    }

### Contact/{id}

The Contact call will let you access an individual corporation's information by including its unique identifier in the call, such as [https://www.usa.gov/api/USAGovAPI/corporate/contacts.json/contact/52999](https://www.usa.gov/api/USAGovAPI/corporate/contacts.json/contact/52999).

### Sample Results

The Contact endpoint will return a single object, such as:

    {
      "Id": "52999",
      "URI": "http://www.usa.gov/api/USAGovAPI/corporate/contacts.json/contact/52999",
      "Language": "en",
      "Name": "Apple Computer, Inc.",
      "Source_Url": "http://www.usa.gov/notpublishable.shtml",
      "Street1": "One Infinite Loop",
      "City": "Cupertino",
      "StateTer": "CA",
      "Zip": "95014",
      "Phone": [
        "408-996-1010"
      ],
      "Tollfree": [
        "1-800-676-2775 (Customer Service)",
        "1-800-275-2273 (iPod, iPad, and Mac Technical Support)",
        "1-800-694-7466 (iPhone Technical Support)"
      ],
      "TTY": [
        "1-877-204-3930"
      ],
      "Web_Url": [
        {
          "Url": "http://www.facebook.com/pages/Apple-Computers/108521342513509",
          "Description": "Apple Computer, Inc. Apple Computer, Inc.s Facebook Page",
          "Language": "en"
        },
        {
          "Url": "http://www.apple.com",
          "Description": "",
          "Language": "en"
        }
      ]
    }

For a complete list of fields returned in the json, see the data model description above. Please note that any field that contains more than one item in it (such as web URLs), is returned as an array and noted in the data model description.

## Terms of Service

By using this data, you agree to the [Terms of Service](https://www.usa.gov/developer-terms-of-service).
