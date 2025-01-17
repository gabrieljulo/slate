
# Introduction
JULO partnership API will help you implement the JULO applying and using credit limit process, with your own app.  documentation will help you as a partner to integrate with JULO

# Use Cases
Applying for credit limit
Customer can be applying for a credit limit, after getting a credit limit customer can use that in every transaction in JULO

# Specifications


## Authentication

JULO Partner credential. This data is generated by JULO Integration Team and is provided  to you upon partner activation.

Registering as a partner with JULO and getting the credentials, you can add a secret key and username in the header every time you hit our endpoint.



<table>
  <tr>
   <td>secret-key
   </td>
   <td>{secret_key}
   </td>
  </tr>
  <tr>
   <td>username
   </td>
   <td>{username}
   </td>
  </tr>
</table>



## Environment

JULO has three environments Staging, UAT, and Production, each environment has a different base URL also partner will give Credentials for each environment.

* Staging base URL : https://api-staging.julofinance.com
* UAT base URL : https://api-uat.julofinance.com
* Production base URL : https://api.julo.co.id


## Request Format

JULO often using JSON format for the request but JULO sometimes using Format-data and query string


## Response format


There will be 2 different formats for response success and failure.

success response:


```
{
    "success": true,
    "data": {some data...},
    "errors": []
}

```


Failure response: \



```
{
    "success": false,
    "data": null,
    "errors": [
        "error message"
    ]
}

```



# API reference


## Applying for credit limit


### initial registration API

Initial registration allows your customer to register in JULO, in this process customer need to input basic data like nik and email, and will check if the customer register in julo \



#### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>api/partnership/v1/customer/
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>username
   </td>
   <td>String
   </td>
   <td>NIK, Number(16)
   </td>
   <td>YES
   </td>
   <td>3203020101930001
   </td>
  </tr>
  <tr>
   <td>pin
   </td>
   <td>String
   </td>
   <td>pin for login to julo app, Number (6)
   </td>
   <td>YES
   </td>
   <td>111222
   </td>
  </tr>
  <tr>
   <td>email
   </td>
   <td>String
   </td>
   <td>valid email
   </td>
   <td>YES
   </td>
   <td>example@test.com
   </td>
  </tr>
  <tr>
   <td>latitude
   </td>
   <td>Float
   </td>
   <td>latitude value
   </td>
   <td>YES
   </td>
   <td>-6.1815657
   </td>
  </tr>
  <tr>
   <td>longitude
   </td>
   <td>Float
   </td>
   <td>longitude value
   </td>
   <td>YES
   </td>
   <td>106.7229445
   </td>
  </tr>
</table>


example making request initial registration API


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner"
    -d "{\"username\": \"3203020101930001\", \"pin\": \"111222\", \"email\": \"example@test.com\", \"latitude\": -6.1815657, \"longitude\": 106.7229445}" \
   POST https://api-staging.julo.co.id/api/partnership/v1/customer

```



#### Response

Upon success, the API will respond with data application xid, email, ktp. you need to save application xid, that value will be use in another API \



```
{
    "success": true,
    "data": {
        "application_xid": 12,
        "email": "example@test.com",
        "ktp": "3203020101930001"
    },
    "errors": []
}

```



### Complete Customer Data API

Complete customer data, in this process customers need to complete customer data like fullname, address, monthly income. etc. customers need to fill in their personal data as completely as possible.


#### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/applications/{application_xid}
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>PATCH
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>fullname
   </td>
   <td>String
   </td>
   <td>fullname
   </td>
   <td>YES
   </td>
   <td>Budi Susanto
   </td>
  </tr>
  <tr>
   <td>birth_place
   </td>
   <td>String
   </td>
   <td>birth place
   </td>
   <td>YES
   </td>
   <td>Jakarta
   </td>
  </tr>
  <tr>
   <td>dob
   </td>
   <td>String
   </td>
   <td>date of birth, date format YYYY-MM-DD
   </td>
   <td>YES
   </td>
   <td>1992-01-01
   </td>
  </tr>
  <tr>
   <td>gender
   </td>
   <td>String
   </td>
   <td>Pria/Wanita
   </td>
   <td>YES
   </td>
   <td>Pria
   </td>
  </tr>
  <tr>
   <td>mother_maiden_name
   </td>
   <td>String
   </td>
   <td>mother's name
   </td>
   <td>YES
   </td>
   <td>Nani
   </td>
  </tr>
  <tr>
   <td>address_street_num
   </td>
   <td>String
   </td>
   <td>address street number
   </td>
   <td>YES
   </td>
   <td>Ds Randupadwngan Rt 01 Rw 01
   </td>
  </tr>
  <tr>
   <td>address_provinsi
   </td>
   <td>String
   </td>
   <td>province
   </td>
   <td>YES
   </td>
   <td>DKI Jakarta
   </td>
  </tr>
  <tr>
   <td>address_kabupaten
   </td>
   <td>String
   </td>
   <td>city
   </td>
   <td>YES
   </td>
   <td>Jakarta Utara
   </td>
  </tr>
  <tr>
   <td>address_kecamatan
   </td>
   <td>String
   </td>
   <td>district
   </td>
   <td>YES
   </td>
   <td>Pademangan
   </td>
  </tr>
  <tr>
   <td>address_kelurahan
   </td>
   <td>String
   </td>
   <td>sub-district
   </td>
   <td>YES
   </td>
   <td>Pademangan Timur
   </td>
  </tr>
  <tr>
   <td>Kodepos
   </td>
   <td>String
   </td>
   <td>postal code
   </td>
   <td>YES
   </td>
   <td>14410
   </td>
  </tr>
  <tr>
   <td>home_status
   </td>
   <td>String
   </td>
   <td>home status
   </td>
   <td>YES
   </td>
   <td>Milik keluarga
   </td>
  </tr>
  <tr>
   <td>dob
   </td>
   <td>String
   </td>
   <td>date of birth, date format YYYY-MM-DD
   </td>
   <td>YES
   </td>
   <td>1992-01-01
   </td>
  </tr>
  <tr>
   <td>marital_status
   </td>
   <td>String
   </td>
   <td>marital status
   </td>
   <td>YES
   </td>
   <td>Lajang
   </td>
  </tr>
  <tr>
   <td>dependent
   </td>
   <td>Integer
   </td>
   <td>dependent count
   </td>
   <td>YES
   </td>
   <td>2
   </td>
  </tr>
  <tr>
   <td>mobile_phone_1
   </td>
   <td>String
   </td>
   <td>mobile phone
   </td>
   <td>YES
   </td>
   <td>081234567899
   </td>
  </tr>
  <tr>
   <td>mobile_phone_2
   </td>
   <td>String
   </td>
   <td>mobile phone
   </td>
   <td>NO
   </td>
   <td>081234567888
   </td>
  </tr>
  <tr>
   <td>close_kin_name
   </td>
   <td>String
   </td>
   <td>Parent name
   </td>
   <td>if marital_status=Lajang, this will mandatory
   </td>
   <td>Tom Smith
   </td>
  </tr>
  <tr>
   <td>close_kin_mobile_phone
   </td>
   <td>String
   </td>
   <td>parent mobile phone
   </td>
   <td>if marital_status=Lajang, this will mandatory
   </td>
   <td>081234567891
   </td>
  </tr>
  <tr>
   <td>spouse_name
   </td>
   <td>String
   </td>
   <td>spouse name
   </td>
   <td>if marital_status=Menikah, this will mandatory
   </td>
   <td>Lina
   </td>
  </tr>
  <tr>
   <td>spouse_mobile_phone
   </td>
   <td>String
   </td>
   <td>spouse mobile phone
   </td>
   <td>if marital_status=Menikah, this will mandatory
   </td>
   <td>081234567898
   </td>
  </tr>
  <tr>
   <td>kin_relationship
   </td>
   <td>String
   </td>
   <td>kin relationship
   </td>
   <td>YES
   </td>
   <td>Saudara kandung
   </td>
  </tr>
  <tr>
   <td>kin_name
   </td>
   <td>String
   </td>
   <td>kin name
   </td>
   <td>YES
   </td>
   <td>Dedi Kartono
   </td>
  </tr>
  <tr>
   <td>kin_mobile_phone
   </td>
   <td>String
   </td>
   <td>kin mobile phone
   </td>
   <td>YES
   </td>
   <td>081234561234
   </td>
  </tr>
  <tr>
   <td>job_type
   </td>
   <td>String
   </td>
   <td>job type
   </td>
   <td>YES
   </td>
   <td>Pegawai swasta
   </td>
  </tr>
  <tr>
   <td>job_industry
   </td>
   <td>String
   </td>
   <td>job industri
   </td>
   <td>this field required if job_type not in  Tidak bekerja, Staf rumah tangga, Ibu rumah tangga, Mahasiswa
   </td>
   <td>Sales / Marketing
   </td>
  </tr>
  <tr>
   <td>job_description
   </td>
   <td>String
   </td>
   <td>job description
   </td>
   <td>this field required if job_type not in  Tidak bekerja, Staf rumah tangga, Ibu rumah tangga, Mahasiswa
   </td>
   <td>Salesman
   </td>
  </tr>
  <tr>
   <td>company_name
   </td>
   <td>String
   </td>
   <td>company name
   </td>
   <td>this field required if job_type not in  Tidak bekerja, Staf rumah tangga, Ibu rumah tangga, Mahasiswa
   </td>
   <td>SD Negeri 2 jakarta
   </td>
  </tr>
  <tr>
   <td>company_phone_number
   </td>
   <td>String
   </td>
   <td>company phone number
   </td>
   <td>this field required if job_type not in  Tidak bekerja, Staf rumah tangga, Ibu rumah tangga, Mahasiswa
   </td>
   <td>021123456
   </td>
  </tr>
  <tr>
   <td>job_start
   </td>
   <td>String
   </td>
   <td>job start, date format YYYY-MM-DD
   </td>
   <td>this field required if job_type not in  Tidak bekerja, Staf rumah tangga, Ibu rumah tangga, Mahasiswa
   </td>
   <td>2007-06-15
   </td>
  </tr>
  <tr>
   <td>payday
   </td>
   <td>Integer
   </td>
   <td>payday, range 1 - 31
   </td>
   <td>this field required if job_type not in  Tidak bekerja, Staf rumah tangga, Ibu rumah tangga, Mahasiswa
   </td>
   <td>1
   </td>
  </tr>
  <tr>
   <td>last_education
   </td>
   <td>String
   </td>
   <td>last education
   </td>
   <td>YES
   </td>
   <td>S2
   </td>
  </tr>
  <tr>
   <td>monthly_income
   </td>
   <td>Integer
   </td>
   <td>monthly income
   </td>
   <td>YES
   </td>
   <td>3000000
   </td>
  </tr>
  <tr>
   <td>monthly_expenses
   </td>
   <td>Integer
   </td>
   <td>monthly expenses
   </td>
   <td>YES
   </td>
   <td>1000000
   </td>
  </tr>
  <tr>
   <td>monthly_housing_cost
   </td>
   <td>Integer
   </td>
   <td>monthly housing cost
   </td>
   <td>YES
   </td>
   <td>500000
   </td>
  </tr>
  <tr>
   <td>total_current_debt
   </td>
   <td>Integer
   </td>
   <td>tota  current debt
   </td>
   <td>YES
   </td>
   <td>300000
   </td>
  </tr>
  <tr>
   <td>bank_name
   </td>
   <td>String
   </td>
   <td>bank name
   </td>
   <td>YES
   </td>
   <td>BANK CENTRAL ASIA, Tbk (BCA)
   </td>
  </tr>
  <tr>
   <td>bank_account_number
   </td>
   <td>String
   </td>
   <td>bank account number
   </td>
   <td>YES
   </td>
   <td>10672272764
   </td>
  </tr>
  <tr>
   <td>loan_purpose
   </td>
   <td>String
   </td>
   <td>loan purpose
   </td>
   <td>YES
   </td>
   <td>Kebutuhan sehari-hari
   </td>
  </tr>
  <tr>
   <td>loan_purpose_desc
   </td>
   <td>String
   </td>
   <td>loan purpose desc
   </td>
   <td>YES
   </td>
   <td>beli susu pamper dll
   </td>
  </tr>
  <tr>
   <td>is_verification_agreed
   </td>
   <td>Boolean
   </td>
   <td>true/false
   </td>
   <td>YES
   </td>
   <td>true
   </td>
  </tr>
  <tr>
   <td>is_term_accepted
   </td>
   <td>Boolean
   </td>
   <td>true/false
   </td>
   <td>YES
   </td>
   <td>true
   </td>
  </tr>
</table>


Before making request complete customer data API there are several API need to call first \



<table>
  <tr>
   <td>API’s
   </td>
   <td>mandatory
   </td>
   <td>description
   </td>
  </tr>
  <tr>
   <td>Image upload
   </td>
   <td>YES
   </td>
   <td>image upload API, this API will be use for upload KTP and selfie images
   </td>
  </tr>
  <tr>
   <td>Bank scrape
   </td>
   <td>NO
   </td>
   <td>bank scrape API, this API will get bank data
   </td>
  </tr>
  <tr>
   <td>BPJS scrappe
   </td>
   <td>NO
   </td>
   <td>BPJS scrape API, this API will get BPJS data
   </td>
  </tr>
  <tr>
   <td>Send OTP and Validate OTP
   </td>
   <td>YES
   </td>
   <td>those API’s need to hit for validate mobile phone
   </td>
  </tr>
</table>


example making request complete customer data API


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner"
    -d "{\"fullname\": \"budi ismail\", \"birth_place\": \"Jakarta\", \"kin_mobile_phone\": \"087778231801\", \"job_industry\": \"Kesehatan\", \"job_type\": \"Pegawai swasta\", \"job_description\": \"Apoteker\", \"monthly_income\": 10000000, \"monthly_expenses\": 500000, \"monthly_housing_cost\": 0, \"total_current_debt\": 0, \"dob\": \"1992-01-01\", \"gender\": \"Pria\", \"address_street_num\": \"Batcave, Gotham City\", \"address_provinsi\": \"DKI Jakarta\", \"address_kabupaten\": \"Jakarta Barat\", \"address_kecamatan\": \"Cengkareng\", \"address_kelurahan\": \"Cengkareng Barat\", \"address_kodepos\": \"11730\", \"bank_account_number\":\"0672272764\", \"bank_name\":\"BANK NEGARA INDONESIA (PERSERO), Tbk (BNI)\", \"company_name\":\"DBS Bank\", \"dependent\":\"2\",\"home_status\":\"Milik sendiri, lunas\", \"company_phone_number\":\"02153653232\", \"job_start\":\"2010-07-01\", \"mobile_phone_1\": \"085330838909\", \"close_kin_mobile_phone\":\"08533038906\", \"spouse_mobile_phone\":\"085330838901\", \"kin_name\":\"Lawage Nugroho\", \"kin_relationship\":\"Saudara kandung\", \"last_education\":\"Diploma\", \"loan_purpose\":\"Membeli kendaraan\", \"loan_purpose_desc\":\"Need to buy new gadget to repel sharksss\", \"marital_status\":\"Menikah\", \"occupied_since\":\"1999-07-13\", \"payday\":\"24\", \"kin_dob\":\"1978-01-28\", \"spouse_dob\":\"1972-01-28\", \"spouse_name\":\"Jeane Melany\", \"mother_maiden_name\":\"Nani\", \"is_verification_agreed\": true, \"is_term_accepted\": true}"\
   POST https://api-staging.julo.co.id/api/partnership/v1/application/{application_xid}

```



#### Response

Upon success, the API will respond with data customer


```
{
   "success": true,
   "data": {
       "validated_qr_code": false,
       "loan_purpose": "Membeli kendaraan",
       "loan_purpose_desc": "Need to buy new gadget to repel sharks",
       "payday": 24,
       "fullname": "prod only",
       "dob": "1992-01-01",
       "birth_place": "Jakarta",
       "gender": "Pria",
       "ktp": "3203020501960030",
       "address_street_num": "Batcave, Gotham City",
       "address_provinsi": "DKI Jakarta",
       "address_kabupaten": "Jakarta Barat",
       "address_kecamatan": "Bandung Kulon",
       "address_kelurahan": "Cigondewah Kaler",
       "address_kodepos": "40214",
       "occupied_since": "1999-07-13",
       "home_status": "Milik sendiri, lunas",
       "mobile_phone_1": "085330838909",
       "new_mobile_phone": null,
       "mobile_phone_2": null,
       "email": "ari30@julo.co.id",
       "marital_status": "Menikah",
       "dependent": 2,
       "spouse_name": "Jeane Melany",
       "spouse_dob": "1972-01-28",
       "spouse_mobile_phone": "085330838901",
       "kin_name": "Lawage Nugroho",
       "kin_dob": "1978-01-28",
       "kin_gender": null,
       "kin_mobile_phone": "087778231801",
       "kin_relationship": "Saudara kandung",
       "close_kin_name": null,
       "close_kin_mobile_phone": "08533038906",
       "close_kin_relationship": null,
       "job_type": "Pegawai swasta",
       "job_industry": "Kesehatan",
       "job_function": "Bos",
       "job_description": "job_description",
       "company_name": "DBS Bank",
       "company_phone_number": "02153653232",
       "job_start": "2010-07-01",
       "monthly_income": 10000000,
       "last_education": "Diploma",
       "gpa": 2.49,
       "has_other_income": false,
       "other_income_amount": null,
       "other_income_source": null,
       "monthly_housing_cost": 0,
       "monthly_expenses": 500000,
       "total_current_debt": 0,
       "bank_name": "BANK NEGARA INDONESIA (PERSERO), Tbk (BNI)",
       "bank_account_number": "0672272764",
       "application_xid": 2235427695,
       "position_employees": null,
       "employment_status": null,
       "dialect": null,
       "additional_contact_1_name": null,
       "additional_contact_1_number": null,
       "additional_contact_2_name": null,
       "additional_contact_2_number": null,
       "loan_purpose_description_expanded": null,
   },
   "errors": []
}
```



### Additional API’s

Additional API’s will help you to check and get data for complete customer data, you can get address, loan_purpose, banks, etc. some of this API is optional like check strong pin and pre-register check


#### Image Upload API

images upload API will be used for upload image files like KTP and selfie. for this API in the front end need to some guideline to make sure the image is correct


##### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/applications/{application_xid}/images
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>upload
   </td>
   <td>File
   </td>
   <td>Images ktp_self/selfie/ crop_selfie
   </td>
   <td>YES
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>image_type
   </td>
   <td>String
   </td>
   <td>use this field to specify the emage type.
   </td>
   <td>YES
   </td>
   <td>crop_selfie
   </td>
  </tr>
</table>


example images

example making request image upload API using form-data


```
curl \
  -F "image_type=ktp_self" \
  -F "upload=test.jpg" \
POST ://api-staging.julofinance.com/api/partnership/v1/applications/{application_xid}/images
```


Possible image Types:


<table>
  <tr>
   <td><strong>Image Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>ktp_self
   </td>
   <td>Image of KTP
   </td>
  </tr>
  <tr>
   <td>crop_selfie
   </td>
   <td>Image of cropped version of selfie
   </td>
  </tr>
  <tr>
   <td>selfie
   </td>
   <td>Image of original selfie image
   </td>
  </tr>
  <tr>
   <td>bank_statement
   </td>
   <td>Image of bank statement
   </td>
  </tr>
  <tr>
   <td>paystub
   </td>
   <td>Image of paystub
   </td>
  </tr>
  <tr>
   <td>ktp_privy
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>drivers_license_privy
   </td>
   <td>Image of driver’s license
   </td>
  </tr>
  <tr>
   <td>just_selfie_privy
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>foto_kartu_keluraga_privy
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>e_ktp_privy
   </td>
   <td>Image of E-KTP
   </td>
  </tr>
  <tr>
   <td>selfie_privy
   </td>
   <td>Image of selfie with ktp
   </td>
  </tr>
  <tr>
   <td>passport_privy
   </td>
   <td>Image of passport
   </td>
  </tr>
  <tr>
   <td>passport_selfie_privy
   </td>
   <td>Image of selfie with passport
   </td>
  </tr>
</table>



##### Response

Upon success, the API will respond without data, success is true mean success upload image


```
{
   "success": true,
   "data": "success upload image",
   "errors": []
}

```



#### BPJS scrape API

This API will get information about BPJS customer


##### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/bpjs/login/{application_xid}/{app_type}
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>GET
   </td>
  </tr>
</table>


for app_type value, you can chose base on your app, if your app is web base the app_type value is web and if your app is android the app_type value is android


```
curl GET \
https://api-staging.julofinance.com/api/partnership/v1/bpjs/login/{application_xid}/{app_type}
```



##### Response

Upon success, the API will respond with url, customer will use that URL for login to their BPJS account


```
{
    "success": true,
    "data": {
        "url": "https://talosopen.tongdun.net/box/safety/id/bpjs?box_token=6fa9d2a815e746b58ac14b69fefaf60e&passback_params=1000044307_2000045280_android&cb=https%3A%2F%2Fwww.julo.co.id%2F&fix=1",
    },
    "errors": []
}

```



#### Pre-register check API

This API for checking if the customer already register in JULO


##### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/preregister-check
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>nik
   </td>
   <td>String
   </td>
   <td>NIK, numbers(16)
   </td>
   <td>YES
   </td>
   <td>3203020101930001
   </td>
  </tr>
  <tr>
   <td>email
   </td>
   <td>String
   </td>
   <td>google email
   </td>
   <td>YES
   </td>
   <td>example@gmail.com
   </td>
  </tr>
</table>


Example making request


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner"
    -d "{\"nik\": \"3203020101930001\", \"email\": \"example@test.com\"}" \
   POST https://api-staging.julo.co.id/api/partnership/v1/preregister-check

```



##### Response

Upon success, the API will respond with success True mean customer is not register in JULO \



```
{
   "success": true,
   "data": null,
   "errors": []
}

```



#### Check strong API

This API will use for check how the strong pin submitted by customer


##### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/check-strong-pin
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>nik
   </td>
   <td>String
   </td>
   <td>NIK, numbers(16)
   </td>
   <td>YES
   </td>
   <td>3203020101930001
   </td>
  </tr>
  <tr>
   <td>pin
   </td>
   <td>String
   </td>
   <td>numbers(16)
   </td>
   <td>YES
   </td>
   <td>159357
   </td>
  </tr>
</table>


example making request


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner"
    -d "{\"nik\": \"3203020101930001\", \"pin\": \"159357\"}" \
   POST https://api-staging.julo.co.id/api/partnership/v1/check-strong-pin

```



##### Response

Upon success, the API will respond with success True pin is strong


```
{
   "success": true,
   "data": "Strong password",
   "errors": []
}

```



#### Send OTP API

This API will use for sending OTP to customer mobile phone, the OTP has a expiry time


##### Request \



<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/application/otp/{application_xid}
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>phone
   </td>
   <td>String
   </td>
   <td>mobile phone number
   </td>
   <td>YES
   </td>
   <td>0812345601
   </td>
  </tr>
</table>



```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner"
    -d "{\"phone\": \"0812345601\"}" \
   POST https://api-staging.julo.co.id/api/partnership/v1/application/otp/{application_xid}
```



##### Response

Upon success, the API will respond with success is true mean OTP send to customer \



```
{
   "success": true,
   "data": null,
   "errors": []
}

```



#### Validate OTP API

This API will use for validate OTP


##### Request \



<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/application/otp/validate/{application_xid}
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>otp_token
   </td>
   <td>String
   </td>
   <td>otp code
   </td>
   <td>YES
   </td>
   <td>311232
   </td>
  </tr>
</table>


example making request


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner"
    -d "{\"otp_token\": \"311232\"}" \
   POST https://api-staging.julo.co.id/api/partnership/v1/application/otp/validate/{application_xid}
```



##### Response

Upon success, the API will respond with success is true mean OTP is correct and not expiry


```
{
   "success": true,
   "data": null,
   "errors": []
}

```



#### Dropdown data API

This API will get data banks, jobs, vehicle_types loan_purposes, home_statuses, job_types, kin_relationships, last_educations, marital_statuses, vehicle_ownerships, and 'birth_places for complete customer data


##### Request \



<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/dropdown-data
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>GET
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>data_selected
   </td>
   <td>String
   </td>
   <td>You can choose the data you want. this is data selection banks, jobs, job_industries, vehicle_types, loan_purposes, home_statuses, job_types, kin_relationships, last_educations, marital_statuses, vehicle_ownerships, birth_places
   </td>
   <td>YES
   </td>
   <td>loan_purposes
   </td>
  </tr>
  <tr>
   <td>job_industry
   </td>
   <td>String
   </td>
   <td>Value from /api/partnership/v1/dropdown-data?data=job_industries
   </td>
   <td>Mandatory if key data=jobs
   </td>
   <td>Transportasi
   </td>
  </tr>
</table>


example making request


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner" \
   GET https://api-staging.julo.co.id/api/partnership/v1/dropdown -data?data_selected=loan_purposes
```



##### Response

Upon success, the API will respond with data you need


```
{
   "success": true,
   "data": [
       "Modal usaha",
       "Kebutuhan sehari-hari",
       "Membayar hutang lainnya",
       "Biaya pendidikan",
       "Biaya kesehatan",
       "Belanja online",
       "Membeli elektronik",
       "Membeli kendaraan",
       "Biaya liburan / umroh",
       "Renovasi Rumah",
       "kawin lagi",
       "ngepet",
       "beli menyan",
       "Transfer ke Keluarga/Teman"
   ],
   "errors": []
}
```



#### Address API

This API will give you a province, cities, district, sub-district and postal code to complete customer data


##### Request \



<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/address
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>GET
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>get_address
   </td>
   <td>String
   </td>
   <td>You can choose the data you want. this is data selection : province, city, district, sub_district
   </td>
   <td>YES
   </td>
   <td>city
   </td>
  </tr>
  <tr>
   <td>province
   </td>
   <td>String
   </td>
   <td>province
   </td>
   <td>base on get_address value
   </td>
   <td>Jawa Barat
   </td>
  </tr>
  <tr>
   <td>city
   </td>
   <td>String
   </td>
   <td>city
   </td>
   <td>base on get_address value
   </td>
   <td>Bandung
   </td>
  </tr>
  <tr>
   <td>district
   </td>
   <td>String
   </td>
   <td>district
   </td>
   <td>base on get_address value
   </td>
   <td>Andir
   </td>
  </tr>
</table>


example making request for getting cities values


```
curl \
    -H "Content-Type: application/json" \
    -H "secret-key: secret_key_value" \
    -H "username: partner" \
   GET https://api-staging.julo.co.id/api/partnership/v1/address?get_address=city&province=JawaBarat
```



##### Response

Upon success, the API will respond with cities data


```
{
   "success": true,
   "data": [
       "Bandung",
       "Bandung Barat",
       "Banjar",
       "Bekasi",
       "Bogor",
       "Ciamis",
       "Cianjur",
       "Cimahi",
       "Cirebon",
       "Depok",
       "Garut",
       "Indramayu",
       "Karawang",
       "Kuningan",
       "Majalengka",
       "Pangandaran",
       "Purwakarta",
       "Subang",
       "Sukabumi",
       "Sumedang",
       "Tasikmalaya"
   ],
   "errors": []
}
```



#### Bank Scrape API

This API will get information about BPJS customer


##### Request


<table>
  <tr>
   <td>endpoint
   </td>
   <td>/api/partnership/v1/external-data-imports/{application_xid}
   </td>
  </tr>
  <tr>
   <td>method
   </td>
   <td>POST
   </td>
  </tr>
</table>


data:


<table>
  <tr>
   <td>Key
   </td>
   <td>Datatype
   </td>
   <td>Description
   </td>
   <td>Mandatory
   </td>
   <td>Example
   </td>
  </tr>
  <tr>
   <td>data_type
   </td>
   <td>String
   </td>
   <td>Name of bank, option : bri, bca, mandiri, bni
   </td>
   <td>YES
   </td>
   <td>bri
   </td>
  </tr>
  <tr>
   <td>credentials
   </td>
   <td>String
   </td>
   <td>credentials bank account
   </td>
   <td>YES
   </td>
   <td>{‘username’: ‘username_example’, ‘passwor’: ‘password_example’}
   </td>
  </tr>
</table>


Example making request using form-data


```
curl \
  -F "data_type=bri" \
  -F "credentials={'username': 'username_example', 'password': 'password_example'}" \
POST ://api-staging.julofinance.com/api/partnership/v1/external-data-imports/{application_xid}
```



##### Response

Upon success, the API will respond with id, status, application xid and data type


```
{
   "status": "initiated",
   "application_xid": 2210045983,
   "data_type": "bri",
   "id": 4836
}
```

