# Postman API Inspection Notes

## Using Postman to Inspect the API

### 1. API Endpoint
- **URL:** `https://api.linqapp.com/api/v2/cards/ashu_reddy/contact_downloads`
- **Method:** `POST`

### 2. Request Details
#### Headers:
- `Content-Type: application/json`
- `Accept: application/json`
- `X-LINQ-API-TOKEN: null`
- `X-GA: omGfxn7BTdxEoCS9`
- `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36`
- `Referer: https://linqapp.com/`

#### Payload (JSON Body):
```json
{"name":"aaaa","phone_number":"+15131111111","is_accept_marketing":false,"do_not_create_user_contact":true}
```

### 3. Response Details
- **Status Code:** `200 OK`
- **Response Time:** `363 ms`
- **Response Headers:**
  - `access-control-allow-credentials: true`
  - `access-control-allow-methods: GET, POST, PUT, DELETE, OPTIONS`
  - `access-control-allow-origin: https://linqapp.com`
  - `access-control-max-age: 7200`
  - `cache-control: max-age=0, private, must-revalidate`
  - `content-encoding: gzip`
  - `content-type: application/json; charset=utf-8`
  - `date: Thu, 03 Apr 2025 03:42:22 GMT`
  - `etag: W/"fe41c0f4bcd7e36122b67062cbb7b7d3"`
  - `referrer-policy: strict-origin-when-cross-origin`
  - `strict-transport-security: max-age=31536000; includeSubDomains; preload`
  - `vary: Accept, Accept-Encoding, Origin`
  - `x-content-type-options: nosniff`
  - `x-download-options: noopen`
  - `x-frame-options: SAMEORIGIN`
  - `x-permitted-cross-domain-policies: none`
  - `x-request-id: bd81f7a3-7aa6-4264-ac1a-e95ec6971ba5`
  - `x-runtime: 0.037874`
  - `x-xss-protection: 1; mode=block`
- **Response Body:**
```json
  {
  "data": {
    "contact": {
      "id": 2275961,
      "first_name": "aaaa",
      "last_name": "",
      "phone_number": "+15131111111",
      "location": null,
      "email": null,
      "company": null,
      "title": null,
      "image_url": null,
      "deleted_at": null,
      "created_at": "2025-04-02T22:42:21.976-05:00",
      "updated_at": "2025-04-02T22:42:21.976-05:00",
      "synced_via_hr": false,
      "override_hr_synced": true
    },
    "session_uuid": "f2cc9a94-421b-41ad-ae54-f16921b88e61"
  }
}
```



## Simulating Contact Submission and Inspecting Network Activity
- I started by using the browser’s Dev Tools to capture the network request. I went to `https://linqapp.com/ashu_reddy?r=link`, clicked on **"Exchange Contact"**, entered a **name** (`aaaa`) and **phone number** (`+15131111111`), and submitted the form.
- While checking the network log, I found the `POST` request to `https://api.linqapp.com/api/v2/cards/ashu_reddy/contact_downloads`.
- Then, I used Postman to recreate this request by sending a `POST` request to simulate saving a contact. I made sure to copy the headers and payload exactly as they appeared in the network log.
- I double-checked that the headers and payload in Postman matched what I saw in the network log, and they did.
- Finally, I looked at the response data in Postman and compared it to the network log. It lined up well, though the `contact.id` was different as expected since it was a new request (`2276035` in Postman vs. `2275961` in the network log).

## Interesting Findings and Observations
### 1. Response Data
- The response showed that the contact was created successfully, and it gave me a unique `contact_id` (for example, `2275961` in the network log and `2276035` in Postman).
- I noticed that fields like `location`, `email`, `company`, `title`, and `image_url` in the response were all `null`. This probably means these fields aren’t required or automatically filled in when creating a contact.
- The response also included a `session_uuid`, which I think is used to track the session or connect to other requests later.

### 2. Headers & Authentication
- I saw that the `X-LINQ-API-TOKEN` was set to `null`, which means this endpoint doesn’t need authentication and anyone can access it. That makes sense since it’s a feature for visitors, but it made me wonder about security risks (more on that below).
- There was also an `X-GA` header (`omGfxn7BTdxEoCS9`), which looks like it might be a tracking or session ID, maybe for analytics.

### 3. Potential Concerns & Questions
- **Input Validation**: The endpoint let me use a name like `aaaa` without any issues, but I think it should have stricter rules for the `name` field (like only allowing letters, spaces, and hyphens). It should block invalid inputs like `J#$%` or `@@@@@` and return a `400 Bad Request` with a message like `{"error": "Name must contain only letters, spaces, or hyphens"}`.
- **Security Risk**: Since this endpoint doesn’t require authentication, I’m worried it could be abused. For example, someone could spam the API with fake contact submissions. I wonder if there are rate limits or CAPTCHA mechanisms to stop that kind of automated abuse?
- **vCard Download**: I think this endpoint is supposed to trigger an automatic vCard download (related to Bug 002), but the response didn’t include any vCard data. Is the vCard URL sent in a separate request, or is it supposed to be in the response headers (like `Content-Disposition`)?

## Conclusion
- I was able to successfully simulate saving a contact using Postman by sending a `POST` request to `https://api.linqapp.com/api/v2/cards/ashu_reddy/contact_downloads`.
- I made sure the request headers, payload, and response matched what I saw in the network log.
- I found some important things, like the lack of authentication and potential issues with input validation, and I came up with a few questions about security, rate limiting, and how the vCard download works.

### Further Testing Could Include
- I’d like to test how the endpoint handles errors, like what happens if I send invalid payloads (e.g., a malformed phone number or a name with special characters).
- It’d be good to try different payload options, like setting `do_not_create_user_contact` to `false` or `is_accept_marketing` to `true`, to see how that changes things.
- I also want to check if there’s rate limiting by sending a bunch of requests quickly one after another.