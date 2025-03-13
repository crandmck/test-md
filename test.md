## Test of footnotes

The official, open source (MIT licensed) implementation of TrustMark watermarking  for the Content Authenticity Initiative (CAI) as described in  [**TrustMark - Universal Watermarking for Arbitrary Resolution Images**](https://arxiv.org/abs/2311.18297)
[Tu Bui](https://www.surrey.ac.uk/people/tu-bui)[^1], [Shruti Agarwal](https://research.adobe.com/person/shruti-agarwal/)[^2], [John Collomosse](https://www.collomosse.com)[^1] [^2]

[^1]: [DECaDE](https://decade.ac.uk/) Centre for the Decentralized Digital Economy, University of Surrey, UK.

[^2]: [Adobe Research](https://research.adobe.com/), San Jose, CA.

**This repo contains:**
`/python` a Python (3.8.5 or higher) implementation of TrustMark for encoding, decoding and removing image watermarks (using PyTorch).  
`/js` a Javascript implementation of TrustMark decoding of image watermarks (using ONNX)
`/c2pa` a Python example showing how to indicate the presence of a TrustMark watermark in C2PA metadata (manifest)

Models (**ckpt** and **onnx**) are no longer packaged in this repo due to size, but are downloaded upon first use.  Please check the code for [URLs and md5 hashes](https://github.com/adobe/trustmark/blob/4ef0dde4abd84d1c6873e7c5024482f849db2c73/python/trustmark/trustmark.py#L30) if direct download is preferred.

### Quickest start

Install from [PyPi](https://pypi.org/project/trustmark/) directly `pip install trustmark ` and try the code snippet below

### Quick start

Or within the `python/` folder run `pip install .` 

The `python/test.py` script provides examples of watermarking images (a JPEG photo, a JPEG GenAI image, and an RGBA PNG image are provided as examples).  To test the installation the following code snippet in Python shows typical usage:

```python
from trustmark import TrustMark
from PIL import Image

# init
tm=TrustMark(verbose=True, model_type='Q') # or try P

# encoding example
cover = Image.open('images/ufo_240.jpg').convert('RGB')
tm.encode(cover, 'mysecret').save('ufo_240_Q.png')

# decoding example
cover = Image.open('images/ufo_240_Q.png').convert('RGB')
wm_secret, wm_present, wm_schema = tm.decode(cover)

if wm_present:
   print(f'Extracted secret: {wm_secret}')
else:
   print('No watermark detected')

# removal example
stego = Image.open('images/ufo_240_Q.png').convert('RGB')
im_recover = tm.remove_watermark(stego)
im_recover.save('images/recovered.png')
```
In this example, TrustMark variant Q is being used to encode the word `mysecret` in ASCII7 encoding into the image `ufo_240.jpg` which is then decoded, and then removed from the image.

---


