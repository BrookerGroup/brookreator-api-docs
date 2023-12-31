
# RESTful API for Brookreator (2023-11-22)

# To Do List
* [ ] Add more detail for each API endpoint such as posible responses.
* [ ] Add more explanation for each request parameters

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
* [POST /account/files](#post-accountfiles) - General File uploader 
* [GET /account/models](#get-model) - Get all models 
* [GET /account/images?offset=0&limit=500](#get-accountimages) - Get All Images
* [GET /account/favorites?offset=0&limit=500](#get-accountfavorites) - Get All Favorited Images 
* [POST /account/favorites](#post-accountfavorites) - Add Favorite Image
* [DELETE /account/favorites](#delete-accountfavorites)  - Remove Favorite Image
* [POST /t2i/generate](#post-t2igenerate) - Generate Text to Images
* [POST /i2i/trainingImage/:transactionID](#post-i2itrainingImagetransactionID)  - image uploader for AI Portrait training/generating. 
* [GET /i2i/training](#get-i2itraining) - Train images for AI Portrait 
* [POST /i2i/generateImage](#post-i2igenerateimage) - Generate images for AI Portrait 
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

# Themes & Styles Data

- Text to Image Themes 
```json
T2I_Themes : [
  {
    "title": "Flower Field",
    "template":
      "Anime, portrait of a person, light smile, with wind, masterpiece, best quality, movie poster illustration, an extremely delicate, beautifully detailed sunny sky, straw hat, clear sky, epic clouds, farm, beautiful detailed eyes, on the flower field, summer clothes, (fine fabric emphasis:1.4), (watercolor:0.6), (dark brown eyes colour)",
    "src": "flower",
    "negative":
      "EasyNegative, UnrealisticDream, BadDream, bad anatomy, natural skin, blemish, moles, skin spots, crooked teeth, ugly teeth, weird teeth, weird hands, weird arm​, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 4,
    "type": "character",
  },
  {
    "title": "Rainbow Hoodie​",
    "template":
      "pastel chalk paint of a Close portrait of a beautiful woman with No Medium hair and Very Dark eyes, (finely detailed beautiful rainbow eyes: 1.2), wearing future funk hoodie, in a style of funky, rave auroracore background, in photorealism, ultra highres",
    "src": "rainbow",
    "negative":
      "EasyNegative, UnrealisticDream, BadDream, bad anatomy, natural skin, blemish, moles, skin spots, crooked teeth, ugly teeth, weird teeth, weird hands, weird arm​,multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 4,
    "type": "character",
  },
  {
    "title": "Hunter",
    "template":
      "a female monster hunter hunting monsters, baroque, close-up cinematic shot, golden hour, bokeh,  awestruck, concept art, epic,  (masterpiece, side lighting, finely detailed beautiful eyes: 1.2), Best quality, masterpiece, ultra high res",
    "src": "hunter",
    "negative":
      "EasyNegative, multiple bodies, extra heads, extra arms, extra legs, distorted, ugly, (morbid), ((mutilated)), bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), watermarks, nudity, nsfw, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 60,
    "aesthetic": 4,
    "type": "character",
  },
  {
    "title": "Biker",
    "template":
      "a blonde woman biker in a black leather jacket and white tank top inside in a style of comic animation, colourful, chroma aberration, realism, romanticism, retro high saturated colour, Leica prime lenses, retro-futuristic",
    "src": "rider",
    "negative":
      "EasyNegative, multiple bodies, extra arms, extra legs, distorted, ugly, unrealistic, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 4,
    "type": "character",
  },

  {
    "title": "Lazy Peach​",
    "template":
      "8k product shot of a peach iced tea, background is peach tree, digital photography, masterpiece, side lighting, finely detailed: 1.2, hdr, arrange sliced peaches, mint leaves, and other fresh ingredients into a visually appealing centerpiece around the rimmed glass containing the refreshing drink",
    "src": "peach",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 4,
    "type": "product_shot",
  },
  {
    "title": "Futuristic Car",
    "template":
      "futuristic cars, Automotive photography, on the road, light trail, urban city, automotive advertisement, car advertisement, night time, hyper-realistic, high res, 8k, beautiful view, masterpiece, beautiful sky, a sky full of stars, futuristic lighting, cinematics shot, scifi cinematic lighting",
    "src": "futuristic",
    "negative":
      "EasyNegative, unrealistic, ugly, multiple shot, 2 cars, multiple cars, split images",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 10,
    "type": "product_shot",
  },
  {
    "title": "Dreamy Globe",
    "template":
      "a dreamy sceniery with a cat in a snow globe Inside there are elements of dreamy objects such as pink clouds, a yellow",
    "src": "dreamy",
    "negative":
      "EasyNegative, multiple bodies, extra arms, extra legs, distorted, ugly, unrealistic, extra tails, extra limbs, deform, distorted, human, anime",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 30,
    "aesthetic": 7,
    "type": "product_shot",
  },

  {
    "title": "Thai Contemporary",
    "template":
      "The landscape of a Thai modern contemporary wood house surrounded by a lot of exotic flowers, near the brook, water-fall, photo-realistic style, ultra high res, bright, cinematic, concept art, volumetric lighting, intricate details, highly detailed",
    "src": "contemporary",
    "negative":
      "EasyNegative, multiple bodies, extra arms, extra legs, distorted, ugly, unrealistic, extra tails, extra limbs, deform, distorted, human, anime",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 15,
    "type": "exterior",
  },

  {
    "title": "Homey Café",
    "template":
      "Create a space that seamlessly merges organic shapes, natural materials, and a soft color palette to transport customers into a zen-like atmosphere perfect for deep conversations over exquisite coffee",
    "src": "homey",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 26,
    "aesthetic": 8,
    "type": "interior",
  },
  {
    "title": "Bedroom in Rome",
    "template":
      "Italian stone wall style interior design bedroom, brick wall, masterpiece,ultra high res, bright, cinematic, volumetric lighting, intricate details, highly detailed, near the beach, saturated colour pastel",
    "src": "bedroom",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 25,
    "aesthetic": 7,
    "type": "interior",
  },

  {
    "title": "Aquatic Sci-Fi",
    "template":
      "jellyfish in science fiction, post cyberpunk in underwater world with futuristic aurora corals, concept art, fantasy, 8k",
    "src": "aquatic",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 25,
    "aesthetic": 12,
    "type": "sci-fi-fantasy",
  },
  {
    "title": "Utopia",
    "template":
      "Imagine a cutting-edge utopian society built among clouds and floating islands, powered by gleaming solar panels and bioluminescent, daytime",
    "src": "utopia",
    "negative": "",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 25,
    "aesthetic": 7,
    "type": "sci-fi-fantasy",
  },
  {
    "title": "Wonderland",
    "template":
      "Enter a dreamlike realm where fantastical creatures frolic amidst ethereal landscapes, complete with towering mushrooms, sparkling fountains, and delicate steam punk-inspired details.",
    "src": "wonderland",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 30,
    "aesthetic": 7,
    "type": "sci-fi-fantasy",
  },
  {
    "title": "Ancient Ruins",
    "template":
      "a tropical forest, humid air, cinematic shot, masterpiece, amazon, realistic, shooting game, vines, digital art, concept art, ancient temple ruins, with ((glowing blue colour ancient runes engraved on the temple)), light rain",
    "src": "ancient",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 30,
    "aesthetic": 7,
    "type": "sci-fi-fantasy",
  },
  {
    "title": "Space Explorer",
    "template":
      "spaceship parked in a wide dessert with a sky full of stars, Milky Way, vibrant retro style colour, small spacecraft, prehistoric art, art nouveau, intricately designed, lucid, mysterious, fantastic",
    "src": "space",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 25,
    "aesthetic": 7,
    "type": "sci-fi-fantasy",
  },

  {
    "title": "Watercolor",
    "template":
      "watercolor of a landscape on white paper, pastel colors, (ink:1.3), autumn lights, 8k, best quality, (masterpiece:1.2), (best quality:1.0), (ultra highres:1.0)",
    "src": "watercolor",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 20,
    "aesthetic": 7,
    "type": "art",
  },
  {
    "title": "Proto type Sketch",
    "template":
      "a 2D pencil blueprint line art sketch of a vintage car structure on brown paper, (ink:1.3), masterpiece",
    "src": "proto type",
    "negative": "EasyNegative, unrealistic, deform, morbid",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 50,
    "aesthetic": 4,
    "type": "art",
  },

  {
    "title": "Birthday Cat",
    "template":
      "a fluffy cat animal, birthday card, cake, (pastel), realistic, masterpiece, 8k",
    "src": "birthday",
    "negative": "EasyNegative, human, people, women",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 30,
    "aesthetic": 10,
    "type": "holiday",
  },
  {
    "title": "Christmas",
    "template":
      "christmas holiday in the village with the mesmerizing display of the Aurora Borealis dances across the night sky, snowing, well-decorated Christmas tree with red and green bell colors, casting shimmering curtains of colours upon snow-covered peaks and evergreen forests. mistletoes, snow flakes",
    "src": "christmas",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 30,
    "aesthetic": 7,
    "type": "holiday",
  },
  {
    "title": "Lunar Year",
    "template":
      "peony flowers in an ancient Japanese vase, with a cute white rabbit, natural materials, stunning detailed scene, window in the background, wide shot, bright soft diffused light, glow, concept art, intricate, highly detailed, volumetric lighting, masterpiece, hdr, 8k",
    "src": "lunar",
    "negative":
      "EasyNegative, multiples, duplicate, deform, extra, Deep Negative, bad_prompt_version2, bad-artist, bad-artist-anime, bad-quality, nudity, nsfw",
    "model": "revAnimated_v122",
    "sampler": "k_euler_ancestral",
    "steps": 60,
    "aesthetic": 7,
    "type": "holiday",
  },
],
```
- Ai-Portrait Styles
```json
AI_Portrait_Styles : [
  {
    "title": "Korean",
    "src": "koreanAI",
    "template": [
      "((8k half body)) portrait of person, ponytail hair, short hair, long hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, surreal photograph, wearing Uniqlo, (light​ grey blue pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
      "((8k half body)) portrait of person, short hair, smile, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, surreal photograph, wearing Uniqlo, (light blue grey pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, ponytail hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, surreal photograph, wearing Uniqlo, (light​ grey blue pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, long hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, surreal photograph, wearing Uniqlo, (light grey blue pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, long hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white smile turtle neck, (pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, curly hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white dress, smile, at outdoor, (pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, long hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white dress, smile, at outdoor, (pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, ponytail hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white dress, (pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
      "((8k half body)) portrait of person, long hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, surreal photograph, wearing Uniqlo, (light grey blue pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
      "((8k half body)) portrait of person, ponytail hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white suit , (pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>​",
      "((8k half body)) portrait of person, long hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white turtle neck, (light grey brown pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
      "((8k half body)) portrait of person, curly hair, ((shiny skin)), with makeup, colored lip gloss, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, (masterpiece, soft light, finely detailed beautiful eyes: 1.2), hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2),(portrait shot:1.3), intricate, highly detailed, digital photography, art by artgerm and ruan jia and greg rutkowski surreal photograph, wearing a white dress, (pastel color background), <lora:KimYooJung:0.7> <lora:CustomModel:0.7>",
    ],
    "negative": [
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace​",
    ],
    "model": [
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
      "magmix_v6",
    ],
    "sampler": [
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
      "Euler",
    ],
    "steps": [50, 50, 50, 50, 50, 50, 50, 50, 50, 50, 50, 50],
    "aesthetic": [4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4],
    "width": 640,
    "height": 800,
    "poses": [
      "poses2",
      "poses2",
      "poses3",
      "poses4",
      "poses5",
      "poses6",
      "poses7",
      "poses8",
      "poses9",
      "poses10",
      "poses11",
      "poses12",
    ],
    "numRandoms": 0,
    "numPersons": 1,
    "selectTheme": true,
  },
  {
    "title": "Anime",
    "src": "animeAI",
    "template": [
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, beautifully detailed sunny sky, straw hat, clear sky, epic clouds, farm, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, beautifully detailed night sky, hat, night sky, in the city, night market, light smile, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful cold-toned clothing, in a photo-realistic style, ultra high res, beautifully detailed beautiful night sky, in snow, winter wonderland, a hut in the background, forest in the mountain, light smile, perfect holiday, beautiful eyes, winter clothes, snowman, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in white clothing, in a photo-realistic style, ultra high res, beautifully detailed, at the beach, under the sun, sunny day, light smile, ocean, glistening sands, beautiful eyes, thin linen white shirt, glistening glowing skin, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, in a retro interior design, pastel tone, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, beautiful sky, sun bright, warm-toned landscape, clear sky, field of sunflowers, Butterflies resting on the flowers, cottage with flowers in the background, light smile, perfect holiday, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, science fiction, post-cyberpunk background, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colourful streetwear black turtle neck inside, colourful hair,  in a photo-realistic style, colourful hair, ultra high res, beautifully detailed graffiti wall, graffiti painter, colourful wall graffiti, lollipop, hair tied, urban, awesome, cool, artistic weekends, beautiful eyes, streetwear, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
      "Portrait of a caucasian beautiful woman in a style of retro, dressed in colorful warm-toned clothing, in a photo-realistic style, ultra high res, beautifully detailed sunny sky, straw hat, clear sky, epic clouds, farm, by Wes Anderson, bright, cinematic, tableau shot, head-on camera angle, harmonious color palettes, (high quality), close up on face, <lora:CustomModel:0.9>",
    ],
    "negative": [
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
      "canvas frame, cartoon, 3d, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, (((long neck))), signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two person, two people",
    ],
    "model": [
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
      "tiramoesu_v1",
    ],
    "sampler": [
      "Euler a",
      "Euler a",
      "Euler a",
      "Euler a",
      "Euler a",
      "Euler a",
      "Euler a",
      "Euler a",
      "Euler a",
    ],
    "steps": [50, 50, 50, 50, 50, 50, 50, 50, 50],
    "aesthetic": [4, 4, 4, 4, 4, 4, 4, 4, 4],
    "width": 640,
    "height": 800,
    "poses": [],
    "numRandoms": 0,
    "numPersons": 1,
    "selectTheme": false,
  },
]
```
- VideoToVideo Styles
```json
VideoToVideo_Styles : [
  {
    "title": "AI Face",
    "src": "cartoonvdo",
    "template":
      "(best quality, masterpiece, perfect face, beautiful and 'aesthetic':1.2, colorful, dynamic angle, highest detailed face), (official art, extreme detailed, highest detailed)",
    "negative": "EasyNegative, FastNegativeV2",
    "model": "cardosAnime_v20",
    "sampler": "DPM++2Mkarras",
    "steps": 30,
    "aesthetic": 7,
    "poses": "poses1",
    "numRandoms": 0,
    "numPersons": 1,
    "numPersons": 1,
    "strength": 0.35,
    "selectTheme": true,
  },
]
```
- AI QR code Theme
```json

QR_Themes : [
  {
    "title": "Christmas tree",
    "template":
      "(worst quality, low quality:1.4), watermark, signature, monochrome, bad anatomy, bad proportions, negative_hand-neg, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two face, girl, women, EasyNegative​",
    "src": "QRThemes13",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.6,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Jade Dragon ​",
    "template":
      "a mesmerizing mixed media artwork that intricately put together traditional 'aesthetic's of Chinese beautiful nature. a combination that deliberately indicate peace and equilibium. the building's details exudes with elegance, while traditional elements such as an eminent detail of carved wall add a touch of jade, ethereal shiny glow, enveloping the scene in a magical ambiance that blurs the boundaries between dragon and imagination, surreal, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), intricate, highly detailed, jade on dark background",
    "src": "QRThemes1",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.8,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Joan Miro",
    "template":
      "surrealist painting by Joan Miro, abstract shapes, contrast color, primary colors, light color background, 4k resolution, high detailed, Digital painting, art by clive barker, h, r, Giger, and brom,  digital painting, volumetric lighting,",
    "src": "QRThemes2",
    "negative":
      "neon color, watermark, signature, text, two people, two faces, extra fingers, mutated hands, poorly drawn eyes, mutation, deformed, dehydrated, bad anatomy, bad proportions, cloned face, disfigured, gross proportions, malformed limbs, missing arms, missing legs, missing fingers, extra arms, extra legs, fused fingers, too many fingers, long neck, incoherent, draw, logo, text, watermark, signature",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.95,
    "steps": 25,
    "aesthetic": 13,
  },
  {
    "title": "Neon camouflage",
    "template":
      "Neon lights reflect off the sleek, angular surfaces of a cyberpunk metropolis, casting a kaleidoscope of colors across the dark night sky",
    "src": "QRThemes3",
    "negative":
      "(worst quality:2), (low quality: 2),(KHFB, AuroraNegative),(Worst Quality, Low Quality:1.4), human",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.95,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Stormy Night",
    "template":
      "stormy night with lightning exudes fear and yet fascination of nature, a combination of 'aesthetic's from nature and the unpredictability of what's coming, surreal, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), intricate, highly detailed",
    "src": "QRThemes4",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.45,
    "steps": 30,
    "aesthetic": 7,
  },
  {
    "title": "Foodies",
    "template":
      "isometric view of a beef cheesy burger and french fries in abstract combined with art nouveau art style surreal, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4)",
    "src": "QRThemes5",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.45,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Tree house",
    "template":
      "a well design magical massive tree house in the heart of a tropical forest, fascination, intricate design, autumn, golden hour, beautiful and gracious animals around the tree house, birds singing, antlers with the golden horn walking peacefully below the tree house,(masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), depth of field",
    "src": "QRThemes6",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.55,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Galaxy",
    "template":
      "The night sky is reimagined as a canvas for celestial stained glass art, with constellations and galaxies shining bright like diamonds",
    "src": "QRThemes7",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, cartoon, anime, sketches, (worst quality:2), (low quality: 2),(KHFB, AuroraNegative),(Worst Quality, Low Quality:1.4), human",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.95,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Low Poly",
    "template":
      "a cute little matte low poly isometric {tropical island}, erupting volcano, mist, lat lighting, soft shadows, trending on artstation, 3d render, fez video game",
    "src": "QRThemes8",
    "negative": "ugly, disfigured, low quality, blurry, nsfw",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.6,
    "steps": 25,
    "aesthetic": 7,
  },
  {
    "title": "Maneki Neko",
    "template":
      "a portrait of porcelain maneki neko lucky cat surrounded with glistening white in a style of art nouveau and modernism, volumetric lighting, hdr, (masterpiece, soft light, finely detailed, hdr, (high quality:1.4), (ultra highres:1.2), (photorealistic:1.4), (8k, RAW photo:1.2), depth of field",
    "src": "QRThemes9",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.65,
    "steps": 35,
    "aesthetic": 7,
  },
  {
    "title": "Cyberpunk",
    "template":
      "Portrait of a Cyberpunk woman with outfit on neon tokyo rooftop by Greg Rutkowski, Sung Choi, Mitchell Mohrhauser, Maciej Kuciara, Johnson Ting, Maxim Verehin, Peter Konig, final fantasy, mythical, 8k photorealistic, cinematic lighting, HD, high details, atmospheric,",
    "src": "QRThemes11",
    "negative":
      "cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((extra barrel)),((close up)),((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame, ugly, extra limbs, (bad anatomy),gross proportions, (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), mutated hands, (fused fingers), (too many fingers), (((long neck))), (((tripod))), (((tube))), Photoshop, video game, ugly, tiling, poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, mutated, extra limbs, extra legs, extra arms, disfigured, deformed,cross-eye, body out of frame, blurry, bad art, bad anatomy, 3d render, (((umbrella))), (((nsfw))),((Wireframe)),Polygons,Screenshot,Character design,Software,UI,watermark,signature",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.6,
    "steps": 20,
    "aesthetic": 6,
  },
  {
    "title": "Neon Sci-fi Lady",
    "template":
      "a portrait of an astonishing goddess wearing futuristic robot iridescent neon lacy clothes, a perfect face, dark eyes, oil on canvas, masterpiece, expert, insanely detailed, 4k resolution, Stanley Lau Artgerm, high res, hyper-realistic, enchanted, delicate face, with neon hair",
    "src": "QRThemes12",
    "negative":
      "((nudity)), bad_pictures, (bad_prompt_version2:0.8), EasyNegative, 3D, cartoon, anime, sketches, (worst quality:2), (low quality: 2), people, hand, head, blur, blurry, out of frame, duplicate, watermark, signature, text, (((person))), (((human))), (((woman))), bad framing, out of frame, cropped, deformed, ugly, bad quality, error, watermark",
    "model": "RevAnimated_v122",
    "sampler": "k_euler_ancestral",
    "control_weight": 1.65,
    "steps": 30,
    "aesthetic": 7,
  },
];

```

Thumbnail images for theme and styles.
: https://brookergroup-my.sharepoint.com/:f:/p/natheenont/EtG_RgxwhyBJh0NZlEB0nLAB9SiyBy7l1cvLzh5IfKN1cQ?e=8vdJi3

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

### GET /account/models

#### Description:
Get All Models

#### Query:
-

#### Response:
```json
[
  {
    "training_id": "9e299ddd-4287-4803-82af-5bbc08fd8cd8",
    "name": "Model1",
    "cover_image": "https://brookreator-image-training-dev.s3.ap-southeast-1.amazonaws.com/ca377ec9-e094-4dda-b355-52cbb766d056/9e299ddd-4287-4803-82af-5bbc08fd8cd8/de80291a-4873-4c0d-939b-c95c80caf5be.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=AKIAT762APTT5JUTQEXE%2F20231222%2Fap-southeast-1%2Fs3%2Faws4_request\u0026X-Amz-Date=20231222T050943Z\u0026X-Amz-Expires=3600\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=21c498494305298358f6e60415ac47dc2bfac26bfe291f6b18def7d04be5896c",
    "status": "DONE"
  }
]
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


### POST /i2i/generateImage/:transactionID

#### Description:

#### Query:
```json
{
  "images": [],
  "styles": [
    "a close-up portrait of a woman wearing Christmas winter clothes, a Christmas holiday in the snow village, smiling in gratification, great composition, cinematic shot, amazing time, Christmas time, snowing,<lora:CustomModel:0.85>",
    "a close-up portrait of a woman,wearing a Christmas clothes, a Christmas holiday in the snow village with the aurora dances across the night sky, great composition, cinematic shot, amazing time, smiling in gratification, snowing,<lora:CustomModel:0.85>",
    "a close-up portrait of a woman,wearing a Christmas clothes, a Christmas holiday in the snow village with the aurora dances across the night sky, great composition, cinematic shot, amazing time, smiling in gratification, snowing,<lora:CustomModel:0.85>",
    "a close-up portrait of a woman wearing Christmas winter clothes, gingerbread wonderland with ornaments made of gingerbread cookies and candy canes , smiling in gratification, great composition, cinematic shot, amazing time, Christmas time, snowing, Santa hat, <lora:CustomModel:0.85>",
    "a close-up portrait of a woman wearing Christmas winter clothes, a Christmas holiday in the snow village, smiling in gratification, great composition, cinematic shot, amazing time, Christmas time, snowing,<lora:CustomModel:0.85>"
  ],
  "modelKey": "-",
  "lang": "EN",
  "negatives": [
    "(worst quality, low quality:1.4), watermark, signature, monochrome, bad anatomy, bad proportions, negative_hand-neg, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two face, boy, man",
    "(worst quality, low quality:1.4), watermark, signature, monochrome, bad anatomy, bad proportions, negative_hand-neg, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two face, boy, man",
    "(worst quality, low quality:1.4), watermark, signature, monochrome, bad anatomy, bad proportions, negative_hand-neg, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two face, boy, man",
    "(worst quality, low quality:1.4), watermark, signature, monochrome, bad anatomy, bad proportions, negative_hand-neg, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two face",
    "(worst quality, low quality:1.4), watermark, signature, monochrome, bad anatomy, bad proportions, negative_hand-neg, disfigured, deformed, ((extra limbs)), ((close up)), weird colors, blurry, (duplicate), (morbid), ((mutilated)), (out of frame), extra fingers, mutated hands, poorly drawn hands, poorly drawn face, mutation, ugly, bad anatomy, bad proportions, (cloned face), gross proportions, (malformed limbs), (missing arms), missing legs, extra arms, extra legs, fused fingers, too many fingers, signature, video game, tiling, cross-eye, body out of frame, 3d render, necklace, ((earring)), watermark, signature, text, lace, two face, boy, man"
  ],
  "samplers": [
    "DPM++ SDE Karras",
    "DPM++ SDE Karras",
    "DPM++ SDE Karras",
    "DPM++ SDE Karras",
    "DPM++ SDE Karras"
  ],
  "steps": [
    25,
    25,
    25,
    25,
    25
  ],
  "clip_skips": [
    2,
    2,
    2,
    2,
    2
  ],
  "models": [
    "3dAnimationDiffusion_v10",
    "3dAnimationDiffusion_v10",
    "3dAnimationDiffusion_v10",
    "3dAnimationDiffusion_v10",
    "3dAnimationDiffusion_v10"
  ],
  "aesthetics": [
    7,
    7,
    7,
    7,
    7
  ],
  "width": 640,
  "height": 800,
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
