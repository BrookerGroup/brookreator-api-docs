
# RESTful API for Brookreator (2023-11-20)


# Change log
* 2023-11-22 Updated APIs discription
* 2023-11-21 Created documentation 

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
* [GET /account](#get-account) - Account Info 
* [GET /account/images?offset=0&limit=500](#get-accountimages) - Get All Images
* [GET /account/favorites?offset=0&limit=500](#get-accountfavorites) - Get All Favorited Images 
* [POST /account/favorites](#post-accountfavorites) - Add Favorite Image
* [DELETE /account/favorites](#delete-accountfavorites)  - Remove Favorite Image
* [POST /t2i/generate](#post-t2igenerate) - Generate Text to Images
* [POST /i2i/trainingImage/:transactionID](#post-i2itrainingImagetransactionID)  - image uploader for AI Portrait training/generating. 
* [GET /i2i/training](#get-i2itraining) - Train images for AI Portrait 
* [POST /i2i/generateImage](#post-i2igenerateimage) - Generate images for AI Portrait 
* [POST /account/files](#pst-accountfiles) - File uploader 
* [POST /qrlg/generate](#pst-qrlggenerate) - Generate QR code without AI


# Constructing the request
### POST request
* POST requests require JSON payload (application/json).

### Request headers 
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
Get Account Info

#### Query:
-

#### Response:
```json
{ 
    "name": "xxx yyy",
    "email": "xxx@xxx.com",
    "credit": 825, //remaining credit
    "used": 98 
}
```


### GET /account/images

#### Description:
Get all images/videos

#### Query:
-

#### Response:
```json
{
  "images": [
    {
      "id": 191558,
      "createdAt": "2023-11-21T04:57:52Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "6248db25-bd23-48ac-b553-85bae0127ba9",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/6248db25-bd23-48ac-b553-85bae0127ba9.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/6248db25-bd23-48ac-b553-85bae0127ba9.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=467a6538170c8ed03d923216cbbd4aa45436f29fcdf49581a84affbb678b5c50",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191557,
      "createdAt": "2023-11-21T04:57:52Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "2abd2953-e34a-48be-b1b7-9baf0abe8b40",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/2abd2953-e34a-48be-b1b7-9baf0abe8b40.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/2abd2953-e34a-48be-b1b7-9baf0abe8b40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=0fbf23452e7bedee186a4e9179bd7791f1deeb1cd193a34a9b42360694b3c42f",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191556,
      "createdAt": "2023-11-21T04:57:52Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "c78218d1-ac6c-4ea5-b8f5-c10ee786372b",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/c78218d1-ac6c-4ea5-b8f5-c10ee786372b.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/c78218d1-ac6c-4ea5-b8f5-c10ee786372b.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=08602926d83484ec9297210441dadd16bc29ac1eff4ec0cd5aec61a2dd0521e9",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191555,
      "createdAt": "2023-11-21T04:57:51Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "b0549de0-84b9-4bf3-8626-13e515433c3e",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/b0549de0-84b9-4bf3-8626-13e515433c3e.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/b0549de0-84b9-4bf3-8626-13e515433c3e.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=7ab6c8857ab5e7ddc0cd25c782d5c15b3e11d3d1fc38891fc42f5eba447101ab",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191554,
      "createdAt": "2023-11-21T04:57:51Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "87d9fa6c-30b8-4f12-bc45-2c6174b91722",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/87d9fa6c-30b8-4f12-bc45-2c6174b91722.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/87d9fa6c-30b8-4f12-bc45-2c6174b91722.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=033f24b1353065747da0dcae4b0482dc9ed05f127b624e0e0c9ee1b9bca253a1",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191553,
      "createdAt": "2023-11-21T04:57:51Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "22a24970-0194-4feb-8487-e19f6e45f9f2",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/22a24970-0194-4feb-8487-e19f6e45f9f2.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/22a24970-0194-4feb-8487-e19f6e45f9f2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=ae78b821f85e0102a7779e4ca6dd42483a44b5b99a39498eab7c6fc05eaf35ad",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191552,
      "createdAt": "2023-11-21T04:57:14.707Z",
      "updatedAt": "2023-11-21T04:57:14.707Z",
      "deletedAt": null,
      "imageId": "50c7d05e-4dff-498e-a1b1-66e0267c3dc2",
      "groupId": "b4fa3e15-56a8-4f3e-8382-873485dbfa07",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/50c7d05e-4dff-498e-a1b1-66e0267c3dc2.png",
      "vdoFile": "",
      "prompt": "a portrait of porcelain maneki neko lucky cat surrounded with glistening white in a style of art nouveau and modernism, volumetric lighting, hdr, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), depth of field",
      "engine": "",
      "height": 768,
      "width": 768,
      "diffusion": "k_euler_ancestral",
      "cfgScale": 7,
      "seed": "349082741",
      "negativePrompt": "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
      "feature": "TEXT-TO-IMAGE",
      "isQRCode": true,
      "qrCodeContent": "https://www.brookreator.ai/qr-generator",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/50c7d05e-4dff-498e-a1b1-66e0267c3dc2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=1f4e389b7f5218f42dd04aa3409b2058065d22ea450d8d87554aa17dd7dc3eef",
      "vdoUrl": "",
      "controlNetScale": 1.4
    } 
  ],
  "message": "success"
}
```

### GET /account/favorites

#### Description:
get favorited images/videos

#### Query:
-


#### Response:
```json
{
  "images": [
    {
      "id": 191558,
      "createdAt": "2023-11-21T04:57:52Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "6248db25-bd23-48ac-b553-85bae0127ba9",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/6248db25-bd23-48ac-b553-85bae0127ba9.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/6248db25-bd23-48ac-b553-85bae0127ba9.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=467a6538170c8ed03d923216cbbd4aa45436f29fcdf49581a84affbb678b5c50",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191557,
      "createdAt": "2023-11-21T04:57:52Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "2abd2953-e34a-48be-b1b7-9baf0abe8b40",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/2abd2953-e34a-48be-b1b7-9baf0abe8b40.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/2abd2953-e34a-48be-b1b7-9baf0abe8b40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=0fbf23452e7bedee186a4e9179bd7791f1deeb1cd193a34a9b42360694b3c42f",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191556,
      "createdAt": "2023-11-21T04:57:52Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "c78218d1-ac6c-4ea5-b8f5-c10ee786372b",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/c78218d1-ac6c-4ea5-b8f5-c10ee786372b.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/c78218d1-ac6c-4ea5-b8f5-c10ee786372b.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=08602926d83484ec9297210441dadd16bc29ac1eff4ec0cd5aec61a2dd0521e9",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191555,
      "createdAt": "2023-11-21T04:57:51Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "b0549de0-84b9-4bf3-8626-13e515433c3e",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/b0549de0-84b9-4bf3-8626-13e515433c3e.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/b0549de0-84b9-4bf3-8626-13e515433c3e.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=7ab6c8857ab5e7ddc0cd25c782d5c15b3e11d3d1fc38891fc42f5eba447101ab",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191554,
      "createdAt": "2023-11-21T04:57:51Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "87d9fa6c-30b8-4f12-bc45-2c6174b91722",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/87d9fa6c-30b8-4f12-bc45-2c6174b91722.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/87d9fa6c-30b8-4f12-bc45-2c6174b91722.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=033f24b1353065747da0dcae4b0482dc9ed05f127b624e0e0c9ee1b9bca253a1",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191553,
      "createdAt": "2023-11-21T04:57:51Z",
      "updatedAt": "0001-01-01T00:00:00Z",
      "deletedAt": null,
      "imageId": "22a24970-0194-4feb-8487-e19f6e45f9f2",
      "groupId": "f7ac0235-5f81-4cef-afdc-8d9490c490c5",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/22a24970-0194-4feb-8487-e19f6e45f9f2.png",
      "vdoFile": "",
      "prompt": "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, \u003clora:KimYooJung:0.7\u003e \u003clora:CustomModel:0.7\u003e",
      "engine": "-",
      "height": 500,
      "width": 800,
      "diffusion": "DDIM",
      "cfgScale": 10,
      "seed": "760756777",
      "negativePrompt": "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person​",
      "feature": "IMAGE-TRAINING",
      "isQRCode": false,
      "qrCodeContent": "",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/22a24970-0194-4feb-8487-e19f6e45f9f2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=ae78b821f85e0102a7779e4ca6dd42483a44b5b99a39498eab7c6fc05eaf35ad",
      "vdoUrl": "",
      "controlNetScale": 0
    },
    {
      "id": 191552,
      "createdAt": "2023-11-21T04:57:14.707Z",
      "updatedAt": "2023-11-21T04:57:14.707Z",
      "deletedAt": null,
      "imageId": "50c7d05e-4dff-498e-a1b1-66e0267c3dc2",
      "groupId": "b4fa3e15-56a8-4f3e-8382-873485dbfa07",
      "userId": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda",
      "fileName": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/50c7d05e-4dff-498e-a1b1-66e0267c3dc2.png",
      "vdoFile": "",
      "prompt": "a portrait of porcelain maneki neko lucky cat surrounded with glistening white in a style of art nouveau and modernism, volumetric lighting, hdr, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), depth of field",
      "engine": "",
      "height": 768,
      "width": 768,
      "diffusion": "k_euler_ancestral",
      "cfgScale": 7,
      "seed": "349082741",
      "negativePrompt": "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
      "feature": "TEXT-TO-IMAGE",
      "isQRCode": true,
      "qrCodeContent": "https://www.brookreator.ai/qr-generator",
      "url": "https://brookreator-bucket-prod.s3.ap-southeast-1.amazonaws.com/b1bfce18-b93d-477d-a40c-4a0f40e4ecda/50c7d05e-4dff-498e-a1b1-66e0267c3dc2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTTUFYRRWI6%2F20231121%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231121T050510Z\u0026X-Amz-Expires=86400\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=1f4e389b7f5218f42dd04aa3409b2058065d22ea450d8d87554aa17dd7dc3eef",
      "vdoUrl": "",
      "controlNetScale": 1.4
    } 
  ],
  "message": "success"
}
```

### POST /account/favorites

#### Description:
Add a favorite image

#### Request:
```json
{
  "imageIds": [
    "ceb86098-4dbd-498f-a556-d047d59f9806"
  ]
}
```

#### Response:
```json
 {"message":"success"}
```

### DELETE /account/favorites

#### Description:
Remove a favorite image

#### Request:
```json
{
  "imageIds": [
    "ceb86098-4dbd-498f-a556-d047d59f9806"
  ]
}
```

#### Response:
```json
 {"message":"success"}
```

### POST /t2i/generate

#### Description:
Text to Image generation API
- Text to Image
- QR code with AI

#### Body [Text to Image]:
* `prompt`		**string**		prompt
* `samples`		**int**		    samples is number of generated results  (e.g 1 to 9)
* `height`		**int**		    image height
* `width`       **int**		    image width
* `sampler`     **string**		sampler ['k_euler_ancestral','xx']
* `steps`        **int**		        steps (e.g 1 to 100)
* `cfgScale`     **float**		    cfgScale (e.g 1.0 to 10.0)
* (optional) `seed`  **int**		        seed (e.g 128384784748)
* (optional) `negativePrompt` **string**	negative prompt


#### Body [QR Code with AI]:
* `prompt`		**string**		prompt
* `samples`		**int**		    samples is number of generated results  (e.g 1 to 9)
* `height`		**int**		    image height
* `width`       **int**		    image width
* `sampler`     **string**		sampler ['k_euler_ancestral','xx']
* `steps`        **int**		        steps (e.g 1 to 100)
* `cfgScale`     **float**		    cfgScale (e.g 1.0 to 10.0)
* (optional) `seed`  **int**		        seed (e.g 128384784748)
* (optional) `negativePrompt` **string**	negative prompt
* `isQRCode` **bool**		    set true for QR Code 
* (optional) `initImageFilePath` **string**	 
* `qrCodeFilePath` **string**	require if qrCodeContent is empty	 
* `qrCodeContent` **string**	require if qrCodeFilePath is empty

#### Requedt Example:
for Text to Image
```json
{
  "prompt": "Create a space that seamlessly merges organic shapes, natural materials, and a soft color palette to transport customers into a zen-like atmosphere perfect for deep conversations over exquisite coffee",
  "samples": 6,
  "height": 640,
  "width": 640,
  "sampler": "k_euler_ancestral",
  "steps": 26,
  "cfgScale": 8,
  "seed": 0,
  "negativePrompt": "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
}
```

for QR code with AI
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
`transactionID` random uuid string

#### Request Body:
Form Data (png,jpg image type)

#### Response:
```json
{
    "filePath": "ca377ec9-e094-4dda-b355-52cbb766d056/b704c0c1-ac36-4093-8252-e8e671d7d8f7/cf77567a-f8b7-4cb9-b673-5e592e6f37de.png"
}
```


### POST /i2i/trainingImage/:transactionID

#### Description:
`transactionID` random uuid string

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
  "poses": []
}
```

#### Response:
```json
{
  "message": "success"
}
```


### GET /i2i/training  (models)

#### Description:
Get all training historical

#### Query:
-

#### Response:
```json

```

### POST /account/files

#### Description:
Universal Uploader API
---

#### Request:
Form Data Type

#### Response:
```json
{
    "filePath": "b1bfce18-b93d-477d-a40c-4a0f40e4ecda/91752406-c2e0-48d7-bbc7-488ce1b40cca.png"
}
```
