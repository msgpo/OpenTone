# OpenTone

DTMF encoding/decoding


## Install

```bash
pip install opentone
```

## Usage

Here is a clone of [GoogleTone](https://chrome.google.com/webstore/detail/google-tone/nnckehldicaciogcbchegobnafnjkcne?hl=en)


```python
from opentone import ToneGenerator, ToneDecoder
import pyshorteners as pyshort


def tiny_link(url):
    tinyurl = pyshort.Shortener().tinyurl.short(url)
    # The consant prefix in the TinyURL is standard and can be
    # removed altogether, and added in the receiving station
    URL = "http://tinyurl.com/"
    url = tinyurl[len(URL):]
    return url


url = "https://hellochatterbox.com"
url = tiny_link(url)
wave_file = "chatterbox_encoded.wav"
tone_gen = ToneGenerator()
tone_gen.encode_to_wave(url, wave_file)

decoder = ToneDecoder()
decoded_url = decoder.decode_wave(wave_file)

assert decoded_url == url

print("http://tinyurl.com/" + decoded_url)
```


NOTE: Input wave files should be 8khz mono

convert files with
```bash
ffmpeg -i some_file.mp3 -acodec pcm_s16le -ac 1 -ar 8000 out.wav
```