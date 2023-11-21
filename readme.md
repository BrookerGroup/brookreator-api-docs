
# RESTful API for Brookreator (2023-11-20)


# Change log
* 2018-12-16 Updated documentation
* 2018-08-09 V1 Release

# Table of contents
* [Base URL](#base-url)
* [Endpoint types](#endpoint-types)
* [Constructing the request](#constructing-the-request)
* [API documentation](#api-documentation)
* [Error codes](#error-codes)
* [Rate limits](#rate-limits)

# Base URL
* [Production] The base URL is:  https://apiv2.brookreator.ai
* [Development] The base URL is: https://develop.apiv2.brookreator.ai

# Endpoint types
### Non-secure endpoints
All non-secure endpoints do not need authentication and use the method GET.
* -

### Secure endpoints
All secure endpoints require [authentication](#constructing-the-request) and use the method POST.
* [GET /account](#get-account)
* [GET /account/images?offset=0&limit=500](#post-apimarketbalances)
* [GET /account/favorites?offset=0&limit=500](#post-apimarketplace-bid)
* [POST /account/favorites](#post-apimarketplace-ask)
* [DELETE /account/favorites](#post-apimarketplace-bidtest)
* [POST /t2i/generate](#post-apimarketplace-asktest)
* [POST /i2i/trainingImage/:transactionID](#post-apimarketplace-ask-by-fiat)
* [GET /i2i/training](#post-apimarketcancel-order)



# Constructing the request
### POST request
* POST requests require JSON payload (application/json).

### Request headers (POST)
Authentication requires headers data. Every request to the server must contain the following in the request header:
* Accept: application/json
* Content-type: application/json
* Authorization: Bearer {Access Token from aws cognito}

Ref: https://aws.amazon.com/getting-started/hands-on/build-flutter-mobile-app-part-one/module-one/

Example Headers
```
Accept: application/json;
Content-Type: application/json;
Authorization: Bearer eyJraWQiOiJzR3Bpc0RcL0NRSG5yOFdsc3FsSmtSaHBnbzFFZVhURlI2bUlaaEVrZ2VIQT0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI2ZDJiNTNhMi05ZGUzLTQyZDQtODU5ZS1iMjA0MzkyMTliYzMiLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAuYXAtc291dGhlYXN0LTEuYW1hem9uYXdzLmNvbVwvYXAtc291dGhlYXN0LTFfUGJpa2RmUUFNIiwiY2xpZW50X2lkIjoiMnM3NHZuZ3BwZW9kNjZkZWFqanZvcDA5bGsiLCJvcmlnaW5fanRpIjoiZjU0YjUzNDYtMjcxOC00NWExLWIyODMtNTU3ODdmNWEzZjEyIiwiZXZlbnRfaWQiOiI5YmM5YjgzMC0xY2ZhLTQyZDktYjVkNi04ZmQwODBlOTRkMTYiLCJ0b2tlbl91c2UiOiJhY2Nlc3MiLCJzY29wZSI6ImF3cy5jb2duaXRvLnNpZ25pbi51c2VyLmFkbWluIiwiYXV0aF90aW1lIjoxNjg1NTk0MjA4LCJleHAiOjE2ODczNDcyNjgsImlhdCI6MTY4NzM0MzY2OCwianRpIjoiNzk2NWQ0YWItYmM0Yy00MDg1LWE2YjYtOTYwMDUxY2RhYTU4IiwidXNlcm5hbWUiOiI2ZDJiNTNhMi05ZGUzLTQyZDQtODU5ZS1iMjA0MzkyMTliYzMifQ.RwA0_xOU_OuwKgHraxmUrQzUVwMuuGKAkf3O3wjyfnQVJ1Ba3gBhxwazAIJPKbMRZLOfwa8M2OvkntPmju-7R5hI8tZ7uJsSG_lShbrbqngr_gPdgmm1PFPaB5FvcI3D-EzsSwpTK_qa3B1Ampj6EA8QGhle8E2y8hIC8cBBJmm0KAHWIwMnhd5CanKQ1kT3aQAcZuAX8rN3bmnAo3lISYbL08tlf0xPiR41I22FLHhY68pHDuPOmrmbNTNrvM672ARPLfR2ZEtmPDYFKUYl3EBIafHGtX843GbHbeNJndgWeVBQIdVYa-b3fY_wqEyl8QrQYNZXor4L2-FR7fflSg
```


### Payload (POST)
The payload is always JSON. **Always include timestamp in the payload; use `ts` as the key name for timestamp**.


# API documentation
Refer to the following for description of each endpoint

### GET /account

#### Description:
---

#### Query:
-

#### Response:
```json

```


### GET /account/images

#### Description:
---

#### Query:
-

#### Response:
```json

```

### GET /account/favorites

#### Description:
---

#### Query:
-

#### Response:
```json

```

### POST /account/favorites

#### Description:
---

#### Query:
-

#### Response:
```json

```

### DELETE /account/favorites

#### Description:
---

#### Query:
-

#### Response:
```json

```

### POST /t2i/generate

#### Description:
Text to Image generation API

#### Query:
for Text to Image
```json
{
  "prompt": "Create a space that seamlessly merges organic shapes, natural materials, and a soft color palette to transport customers into a zen-like atmosphere perfect for deep conversations over exquisite coffee",
  "samples": 6,
  "engine": "revAnimated_v122",
  "height": 640,
  "width": 640,
  "sampler": "k_euler_ancestral",
  "steps": 26,
  "cfgScale": 8,
  "seed": 0,
  "negativePrompt": "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
  "controlNetScale": 0,
  "isQRCode": false,
  "initImageFilePath": "",
  "qrCodeFilePath": "",
  "qrCodeContent": ""
}
```

for QR code
```json
{
  "prompt": "a portrait of porcelain maneki neko lucky cat surrounded with glistening white in a style of art nouveau and modernism, volumetric lighting, hdr, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), depth of field",
  "samples": 6,
  "engine": "RevAnimated_v122",
  "height": 768,
  "width": 768,
  "sampler": "k_euler_ancestral",
  "steps": 35,
  "cfgScale": 7,
  "seed": "",
  "negativePrompt": "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
  "controlNetScale": 0,
  "isQRCode": true,
  "initImageFilePath": "",
  "qrCodeFilePath": "",
  "qrCodeContent": "https://www.brookreator.ai/qr-generator"
}
```

#### Response:
```json

```
### POST /i2i/upload/:transactionID

#### Description:
---

#### Query:
-

#### Response:
```json
{
    "filePath": "ca377ec9-e094-4dda-b355-52cbb766d056/b704c0c1-ac36-4093-8252-e8e671d7d8f7/cf77567a-f8b7-4cb9-b673-5e592e6f37de.png"
}
```


### POST /i2i/trainingImage/:transactionID

#### Description:
---

#### Query:
```json
{
  "images": [
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/2dfb4d31-7710-4de5-b2c3-2d0f0e58bcca.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/9d2fcc5c-60e5-4e58-8eda-458056014bdb.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/60c00ce7-b19e-470c-9241-1282858f84aa.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/31e4d985-6609-4f04-9f3d-78214bb81f4e.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/2f6df8ca-2b8a-45b7-83db-2259701125e4.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/0d45aba3-e662-4d31-bf47-85e7c1057412.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/f585e799-67a5-4edb-9247-92a47eda8467.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/012f8857-b625-400b-b068-0e98e06004d7.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/24868e24-2458-4c43-9ad2-91ebf3e8b0cf.png",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/34ef5075-3f72-4e55-8747-2d7cbe1b87b2.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/649fce19-9bad-4d1a-a380-df7a87ac6db2.jpg",
    "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/0f067fe3-afde-445c-9a6a-55b07a99111b/2837219a-8756-4f64-a3d4-3699b7dccf9f.jpg"
  ],
  "styles": [
    "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
    "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
    "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
    "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
    "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
    "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:KimYooJung:0.7> <lora:CustomModel:0.7>"
  ],
  "modelKey": "Model1",
  "lang": "TH",
  "negatives": [
    "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
    "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
    "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
    "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
    "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
    "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​"
  ],
  "samplers": [
    "DDIM",
    "DDIM",
    "DDIM",
    "DDIM",
    "DDIM",
    "DDIM"
  ],
  "steps": [
    80,
    80,
    80,
    80,
    80,
    80
  ],
  "models": [
    "magmix_v6",
    "magmix_v6",
    "magmix_v6",
    "magmix_v6",
    "magmix_v6",
    "magmix_v6"
  ],
  "aesthetics": [
    10,
    10,
    10,
    10,
    10,
    10
  ],
  "width": 800,
  "height": 500,
  "seed": "",
  "poses": [
    
  ]
}
```

#### Response:
```json
{
  "message": "success"
}
```


### GET /i2i/training -> models

#### Description:
---

#### Query:
-

#### Response:
```json

```





{"imageIds":["ceb86098-4dbd-498f-a556-d047d59f9806"]}