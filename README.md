# What Is This?

Shufti Pro is a SaaS, that provides quick and accurate digital identity and document verification. E-KYC using government-issued documents like ID card, passport, driving license and even credit/debit cards, etc. has never been easier. Shufti Pro allows for simple and easy ID checks online, securing the virtual trading platforms and FinTech institutions against scams, frauds and money launderers.


# Basic Setup
## General Requirements
Followings are minimum requirements for SDK:
  

 - Internet connection

Supported architectures in SDK:

 - armeabi-v7a, x86, arm64-v8a, x86_64
## SDK Installation Guide 
### Installation through npm (Expo)
  ```
  $ npm install expo-shuftipro-sdk --save`
``` 

### SDK Installation Guide (React Native)
  ```
  $ npm install react-native-shuftipro-sdk --save`
``` 

### Packages

We find it fair to share our `package.json dependencies`  with you! here are the main dependencies used inside Shuftipro.
*#### Dependencies in Expo

```json
"dependencies": {  
  "base-64": "^0.1.0",  
  "expo": "~38.0.8",  
  "expo-av": "~8.2.1",  
  "expo-camera": "~8.3.1",  
  "prop-types": "^15.7.2",  
  "react": "~16.11.0",  
  "react-native": "https://github.com/expo/react-native/archive/sdk-38.0.2.tar.gz",  
  "react-native-easy-grid": "^0.2.2",  
  "react-native-responsive-screen": "^1.4.1",  
  "react-redux": "^7.2.1",  
  "redux": "^4.0.5",  
  "redux-persist": "^6.0.0",  
  "redux-thunk": "^2.3.0",  
  "expo-permissions": "~9.0.1",  
  "expo-network": "~2.2.1"  
},
```
* #### Dependencies in React Native
```json
"dependencies": {  
   "@react-native-community/netinfo": "^5.9.6",
    "base-64": "^0.1.0",
    "prop-types": "^15.7.2",
    "react": "16.13.1",
    "react-native": "0.63.2",
    "react-native-camera": "^3.36.0",
    "react-native-easy-grid": "^0.2.2",
    "react-native-responsive-screen": "^1.4.1",
    "react-native-video": "^5.1.0-alpha7",
    "react-native-video-helper": "^1.4.4",
    "react-redux": "^7.2.1",
    "redux": "^4.0.5",
    "redux-persist": "^6.0.0",
    "redux-thunk": "^2.3.0" 
},
```

 ## Integration:
 See the sample project provided to learn the most common use. Make sure to build on real device.
 
 *### Expo
 ```
 $ import ShuftiPro from "expo-shuftipro-sdk"
 ```

*### React Native
 ```
 $ import ShuftiPro from "react-native-shuftipro-sdk"
 ```



***Make an instance***  
Instance can be made in two ways. First is by using **clientId** and **secretKey**, other one is by providing **accessToken**.  
You can read more about **accessToken**  [here](https://api.shuftipro.com/api/docs/#access-token)
 



## Verification

In order to get verified, customers will have themselves verified through their mobile phones. They will do it through the merchant's mobile application. Merchant will collect the information and send us the data for verification. The Merchant shall provide us with the proofs(Videos). We will not collect them directly from the user.

*  ## With OCR
In verification with OCR, it means that the merchant has not provided us proofs (images/videos) and also no data in some keys. In this verification Shufti Pro will perform extraction of data from those proofs and finally verify the data.
 ``` js
 export const verificationObj = {  
     reference: "Unique reference",  
     country: "GB",  
     language: "EN",  
     email: "johndoe@example.com",  
     callback_url: "http://www.example.com",  
     face: true,  
     document: {  
              supported_types["passport","id_card","driving_license","credit_or_debit_card"],  
              name: {  
                  first_name: "",  
                  last_name: "",  
                  middle_name: ""  
                  },  
              dob: "",  
              document_number: "",  
              expiry_date: "",  
              issue_date: "",  
              fetch_enhanced_data: "1"  
     },  
     address: {  
               full_address: "",  
               name: {  
                     first_name: "",  
                     last_name: "",  
                     middle_name: "",  
                     fuzzy_match: ""  
                     },  
               supported_types: ["id_card", "utility_bill", "bank_statement"],  
   },  
    consent: {  
         format: "printed",  
         text: "This is a customized text"  
              }  
   
   
 };
 ```

*  ## Without OCR
In verification without OCR, merchant gives us the data in keys as well as all the proofs required then Shufti Pro just have to verify the data. No customer interaction takes place in this kind of verification.

 ``` js
 export const verificationObj = {  
     reference: "Unique reference",  
     country: "GB",  
     language: "EN",  
     email: "johndoe@example.com",  
     callback_url: "http://www.example.com",  
     face: true,  
     document: {  
              supported_types["passport","id_card","driving_license","credit_or_debit_card"],  
              name: {  
                  first_name: "John",  
                  last_name: "Carter",  
                  middle_name: "Doe"  
                  },  
              dob: "1992-10-10",  
              document_number: "2323-5629-5465-9990",  
              expiry_date: "2025-10-10",  
              issue_date: "2015-10-10",  
              fetch_enhanced_data: "1"  
     },  
     address: {  
               full_address: "3339 Maryland Avenue, Largo, Florida",  
               name: {  
                     first_name: "John",  
                     last_name: "Carter",  
                     middle_name: "Doe",  
                     fuzzy_match: "1"  
                     },  
               supported_types: ["id_card", "utility_bill", "bank_statement"],  
   },  
    consent: {  
         format: "printed",  
         text: "This is a customized text"  
              }  
   
   
 };
 ```




 
 
## Usage
```js
<ShuftiPro
          isShow={true}
          requestPayload={verificationObj}
          verificationMode={"video"}
          async={true}
          asyncResponseCallback={(response)=>{
           console.log("Response : ", response)
          }}
         onResponseOkayButton={()=>{console.log("Okay Btn")}}
         cancelBtn={()=>{console.log("Cancel Btn")}}
         accessToken={""}
         basicAuth={{client_id:KEYS.BASIC_AUTH_UNAME,secret_key:KEYS.BASIC_AUTH_PWD }}

/>
```

## Asyncronous Feedback

If async value is set to ****true**** you'll instantly get the user's control back so you don't have to wait for the verification results. When a request is completed you'll automatically get a callback.

 ```sh
async = "true"
```

## Verification Mode

This parameter specifies the types of proof that can be used for verification. If verificationMode value is set to ****image**** SDK will be capturing images. However by default it records videos as proofs for verification.

```sh
verificationMode = "image"
```

## Request Parameters

  

It is important to note here that each service module is independent of other and each one of them is activated according to the nature of request received from you. There are a total of four services which include face, document, address and consent.

  

All verification services are optional. You can provide Shufti Pro a single service or mixture of several services for verifications. All keys are optional too.

*  ## reference
      Required: ****Yes****
     Type: ****string****
     Minimum: ****6 characters****
     Maximum: ****250 characters****

   This is the unique reference ID of request, which we will send you back with each response, so you can verify the request. Only alphanumeric values are allowed. This reference can be used to get status of already performed verification requests.

  

  

*  ## country
   
   Required: ****No****
  Type: ****string****
  Length: ****2 characters****

   Send the 2 characters long [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) country code of where your customer is from. Please consult [Supported Countries](https://github.com/shuftipro/RESTful-API-v1.3/blob/master/off-site_with_ocr/countries.md) for country codes.

  

*  ## language
   
   Required: ****No****
  Type: ****string****
  Length: ****2 characters****

   Send the 2 characters long language code of your preferred language to display the verification screens accordingly. Please consult [Supported Languages](languages.md) for language codes. Default language english will be selected if this key is missing in the request.

  

*  ## email

   Required: ****No****
  Type: ****string****
  Minimum: ****6 characters****
  Maximum: ****128 characters****

   This field represents email of the end-user. If it is missing in a request, than Shuftpro will ask the user for its email in an on-site request.

  

*  ## callback_url

   Required: ****No****
   Type: ****string****
   Minimum: ****6 characters****
   Maximum: ****250 characters****

   During a verification request, we make several server to server calls to keep you updated about the verification state. This way you can update the request status at your end even if the customer is lost midway through the process.

*  ## face

   The easiest of all verifications is done by authenticating the face of the users. In case of face verification, end-user will have to capture video of their face that essentially makes it a selfie verification.

   For ****face verification**** just add the key "face" in data dictionary as ****"face": true****

  

<!-- -------------------------------------------------------------------------------- -->

*  ## document
   Shufti Pro provides document verification through various types of documents. The supported formats are passports, ID Cards, driving licenses and debit/credit cards. You can opt for more than 1 document type as well.

   For ****document verification**** just add key "document" in data dictionary. Here are the additional keys for document

   * <h3>supported_types</h3>
   
     Required: ****Yes****
     Type: ****Array****
     
     |  Supported Types       | 
     | :------------- | 
     |  passport | 
     |  id_card  | 
     |  driving_license  |
     |  credit_or_debit_card  |

     ****Example 1**** ["driving_license"]
     ****Example 2**** ["id_card", "credit_or_debit_card", "passport"]

  

   * <h3>name</h3>

     Required: ****No****
     Type: ****object****

     For a name verification, first_name field is required.

     ****Example 1****  { "first_name" : "John", "last_name" : "Doe" }
     ****Example 2****  { "first_name" : "John", "last_name" : "Doe", "fuzzy_match" : "1"}

  

   * <h4>first_name</h4>

      Required: ****Yes****
      Type: ****string****
      Minimum: ****2 characters****
      Maximum: ****32 chracters****
      Allowed Characters are alphabets, - (dash), comma, space, dot and single             quotation mark.
Example ****John'O Harra****

  

   * <h4>middle_name</h4>

     Required: ****No****
     Type: ****string****
    Minimum: ****2 characters****
    Maximum: ****32 chracters****
Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.
Example ****Carter-Joe****

  

   * <h4>last_name</h4>
   
     Required: ****No****
     Type: ****string****
     Minimum: ****2 characters****
     Maximum: ****32 chracters****

      Allowed Characters are alphabets, - (dash), comma, space, dot and single     quotation mark.
 Example ****John, Huricane Jr.****

  

   * <h4>fuzzy_match</h4>

      Required: ****No****
      Type: ****string****
Value Accepted: ****1****

     Provide 1 for enabling a fuzzy match of the name. Enabling fuzzy matching attempts to find a match which is not a 100% accurate.

  

   * <h3>dob</h3>

     Required: ****No****
     Type: ****string****
     Format: ****yyyy-mm-dd****
     
     Provide a valid date. Please note that the date should be before today.
Example 1990-12-31

  

   * <h3>document_number</h3>

     Required: ****No****
   Type: ****string****
   Minimum: ****2 characters****
    Maximum: ****100 chracters****

     Allowed Characters are numbers, alphabets, dots, dashes, spaces, underscores and commas.
Examples 35201-0000000-0, ABC1234XYZ098

  

    * <h3>issue_date</h3>

      Required: ****No****
      Type: ****string****
       Format: ****yyyy-mm-dd****

      Provide a valid date. Please note that the date should be before today.
      Example 2015-12-31

  

   * <h3>expiry_date</h3>

     Required: ****No****
     Type: ****string****
     Format: ****yyyy-mm-dd****

     Provide a valid date. Please note that the date should be after today.
     Example 2025-12-31

   * <h3>fetch_enhanced_data</h3>
   
      Required: ****No****
      Type: ****string****
       Accepted value: ****1****

  

     Provide 1 for enabling enhanced data extraction for the document. Shufti Pro provides its customers with the facility of extracting enhanced data features using OCR technology. Now, instead of extracting just personal information input fields, Shufti Pro can fetch all the additional information comprising more than 100 data points from the official ID documents supporting 150 languages. For example height, place_of_birth, nationality, marital_status, weight, etc.(additional charges apply)

      Extrated data will be returned in object under the key additional_data in case of verification.accepted or verification.declined.

     For Details on additional_data object go to [Additional Data](https://api.shuftipro.com/api/docs/#additional-data)

  

<!-- -------------------------------------------------------------------------------- -->

   *  ## address

      Address of an individual can be verified from the document. For ****address
      verification**** just add key "address" in data dictionary. Here are the 
      additional keys for address

       * <h3>supported_types</h3>
       
         Required: ****Yes****
         Type: ****Array****


         |   Supported Types       | 
         | :------------- | 
         |  id_card | 
         | utiltiy_bill   | 
         | bank_statement   | 



            ****Example 1**** [ "utility_bill" ]
            ****Example 2**** [ "id_card", "bank_statement" ]

      * <h3>full_address</h3>

        Required: ****Yes****
        Type: ****string****
        Minimum: ****2 characters****
        Maximum: ****250 chracters****

        Allowed Characters are numbers, alphabets, dots, dashes, spaces,     underscores, hashes and commas.

  

      * <h3>name</h3>

         Required: ****No****
         Format ****object****
         Name verification from an address image, provide first_name as necessary.

        ****Example 1****  { "first_name" : "John", "last_name" : "Doe" }
        ****Example 2****  { "first_name" : "John", "last_name" : "Doe", "fuzzy_match" : "1"}

  

      * <h4>first_name</h4>

        Required: ****Yes****
        Type: ****string****
        Minimum: ****2 characters****
        Maximum: ****32 chracters****

        Allowed Characters are alphabets, - (dash), comma, space, dot and single    quotation mark.
Example ****John'O Harra****

  

      * <h4>middle_name</h4>

         Required: ****No****
        Type: ****string****
        Minimum: ****2 characters****
        Maximum: ****32 chracters****

        Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.
Example ****Carter-Joe****

  

      * <h4>last_name</h4>

        Required: ****No****
       Type: ****string****
        Minimum: ****2 characters****
        Maximum: ****32 chracters****

        Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.
Example ****John, Huricane Jr.****

  

      * <h4>fuzzy_match</h4>

         Required: ****No****
         Type: ****string****
          Value Accepted: ****1****

        Provide 1 for enabling a fuzzy match of the name. Enabling fuzzy matching attempts to find a match which is not a 100% accurate.

  

<!-- -------------------------------------------------------------------------------- -->


*  ## consent

   Customised documents/notes can also be verified by Shufti Pro. Company documents, employee cards or any other personalised note can be authenticated by this module. You can choose handwritten or printed document format but only one form of document can be verified in this verification module. Text whose presence on the note/customized document is to be verified, is also needed to be provided.

   For ****consent verification**** just add key "consent" in data dictionary. Here are the additional keys for consent

   * <h3>format</h3>
   
       Required: ****Yes****
      Type: ****string****

  
      Text provided in the consent verification can be verified by handwritten documents or printed documents. If “any” is mentioned in the format parameter, then user can verify provided note using either of these two documents. Mention only one format from the following list.
   
      |   Formats       | 
      | :------------- | 
      |  handwritten | 
      | printed   | 
      | any   | 

       
       ****Example 1****  "printed"
       ****Example 2****  "any"

  

  

    * <h3>text</h3>
    
        Required: ****Yes****
        Type: ****string****
        Minimum: ****2 characters****
        Maximum: ****100 chracters****

      Provide text in the string format which will be verified from a given proof.
 

## Response Status Codes

Shufti Pro Verification API uses conventional HTTP response codes to indicate the success or failure of an API request. Every response is generated in JSON with a specific HTTP code.

  

## HTTP Codes

  

Following is a list of HTTP codes which are generated in responses by Shufti Pro Verification API.

  



   HTTP code | HTTP message | Message  |
 | :------------- | :------------- | :------------- | 
   200 | OK | success
   400 | Bad Request  | bad request: one or more parameter is invalid or missing
   401 | Unauthorized | unauthorized: invalid signature key provided in the request
   402 | Request Failed | invalid request data: missing required parameters
   403 | Forbidden  | forbidden: service not allowed
   404 | Not Found  | resource not found
   409 | Conflict | conflicting data: already exists
   500 | Server Error | internal server error

  

  

## Events

  

Events are sent in responses which show the status of request. These events are sent in both HTTP and callback responses.

  Event | description | HTTP Response | Callback Response
| :------------- | :------------- | :------------- | :------------- | 
request.pending | Request parameters are valid and verification url is generated in case of on-site verification.|Yes|Yes
request.invalid | Request parameters provided in request are invalid.|Yes|Yes
request.cancelled | Request is cancelled by the user. This event occurs when end-user disagrees to terms and conditions before starting verifications.|Yes|Yes
request.timeout | Request has timed out after a specific period of time.|No|Yes
request.unauthorized  | Request is unauthorized. The information provided in authorization header is invalid.|Yes|No
verification.accepted | Request was valid and accepted after verification.|Yes|Yes
verification.declined | Request was valid and declined after verification.|Yes|Yes

  

  

## Sample project setup

In ViewController.swift add your ****Client ID**** on line 14 and ****Secret Key**** on line 15, thats it!

>  ****_Note:_**** _Run project on real device._

  

## Test IDs

Shufti Pro provides the users with a number of test documents. Customers may use these to test the demo, instead of presenting their actual information. <br><br>

  

  

[![](https://raw.githubusercontent.com/shuftipro/integration-guide/master/assets/realFace.jpg?v=1)](https://raw.githubusercontent.com/shuftipro/integration-guide/master/assets/realFace.jpg?v=1)

  

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-id-card.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-id-card.jpg)

  

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-id-card.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-id-card.jpg)

  

## Contact

If you have any questions/queries regarding implementation SDK please feel free to contact our [tech support](mailto:support@shuftipro.com).

  

## Copyright

2016-20 © Shufti Pro Ltd.
  
