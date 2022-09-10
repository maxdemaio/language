# Anki

This directory contains information on how I format my anki cards.

---

## Chimera Card

A chimera card that can be either a word/sentence. Note, I tag cards if they can be categorized. I explain this in the Anki section of the website of this repository. If a sentence/context is provided in the `context` field, it will be a sentence card. If a sentence/context is not present, it will be a word card:

```html
<div class="front">
  <!--Show context if context-->
  {{#context}} {{context}} {{/context}}
  <!--Show word if no context-->
  {{^context}} {{word}} {{/context}}
</div>
```

The front template I use is [chimeraFront.html](./chimeraFront.html).

The back template I use is [chimeraBack.html](./chimeraBack.html).

The fields I use are:

1. context
2. word
3. Back
4. POS
5. image
6. wordAudio
7. contextAudio
